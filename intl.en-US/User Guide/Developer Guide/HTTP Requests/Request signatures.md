# Request signatures

You must sign all HTTP or HTTPS API requests to ensure security. Alibaba Cloud Server Load Balancer \(SLB\) uses the request signature to verify the identity of the request sender. SLB implements symmetric encryption with an AccessKey pair to verify the identity of the request sender. An AccessKey pair consists of an AccessKey ID and an AccessKey secret.

You must add the signature to the RPC API request in the following format:

```
https://Endpoint/?SignatureVersion=1.0&SignatureMethod=HMAC-SHA1&Signature=CT9X0VtwR86fNWSnsc6v8YGOjuE%3D&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf
```

where:

-   SignatureMethod: the encryption method of the signature string. Set the value to HMAC-SHA1.
-   SignatureVersion: the version of the signature encryption algorithm. Set the value to 1.0.
-   SignatureNonce: a unique, random number used to prevent replay attacks. You must use different random numbers for different requests. We recommend that you use universally unique identifiers \(UUIDs\).
-   Signature: the signature string generated by symmetrically encrypting the request by using the AccessKey secret.

## AccessKey descriptions

An AccessKey pair is an identity credential that is issued to Alibaba Cloud accounts and RAM users. Each AccessKey pair is used in a similar way as the username and password. AccessKey pairs are used to call API operations. Usernames and passwords are used to log on to the Elastic Compute Service \(ECS\) console. The AccessKey ID is used to verify the identity of the user, while the AccessKey secret is used to encrypt and verify the signature string. You must keep your AccessKey secret confidential. For more information, see [Obtain an Access Key](/intl.en-US/User Guide/Developer Guide/Obtain an Access Key.md).

**Note:** SLB provides SDKs for multiple programming languages, including third-party SDKs. This simplifies signature signing. For more information, download [SDKs](https://github.com/aliyun).

## Step 1: Create a canonicalized query string

```
GET&%2F&AccessKeyId%3Dtestid%26Action%3DDescribeRegions%26Format%3DXML%26SignatureMethod%3DHMAC-SHA1%26SignatureNonce%3D3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf%26SignatureVersion%3D1.0%26TimeStamp%3D2016-02-23T12%253A46%253A24Z%26Version%3D2014-05-26
```

1.  Create a canonicalized query string by arranging the request parameters in alphabetical order. The request parameters include all common parameters and operation-specific parameters except Signature.

    **Note:** If you use the GET method to send a request, the request parameters are included as a part of the request URL. The first parameter follows the question mark \(`?`\) in the URL, and the other parameters follow an ampersand \(`&`\).

2.  Encode the canonicalized query string in UTF-8. Encode the request parameters and parameter values by using the UTF-8 character set and following the [RFC 3986](http://tools.ietf.org/html/rfc3986) specification. The following encoding rules are used:
    -   Do not encode uppercase letters, lowercase letters, digits, and the following special characters: hyphens \(-\), underscores \(\_\), periods \(.\), and tildes \(~\).
    -   Other characters must be percent-encoded in the `%XY` format. `XY` represents the ASCII code of the character in hexadecimal notation. For example, double quotation marks \(`"`\) are encoded as `%22`.
    -   Extended UTF-8 characters are encoded in the `%XY%ZA...` format.
    -   Space characters must be encoded as `%20`. Do not encode space characters as plus signs \(`+`\).

        The preceding encoding method is slightly different from the `application/x-www-form-urlencoded` MIME-type encoding algorithm.

        If you use `java.net.URLEncoder` in the Java standard library, use `percentEncode` to encode request parameters and their values. In the encoded query string, replace the plus sign \(`+`\) with `%20`, the asterisk \(`*`\) with `%2A`, and `%7E` with a tilde \(`~`\). This way, you can obtain an encoded string that matches the preceding encoding rules.

        ```
        private static final String ENCODING = "UTF-8";
        private static String percentEncode(String value) throws UnsupportedEncodingException {
        return value ! = null ? URLEncoder.encode(value, ENCODING).replace("+", "%20").replace("*", "%2A").replace("%7E", "~") : null;
        }
        ```

3.  Concatenate the encoded parameter names and values with equal signs \(`=`\).
4.  Sort the parameter name and value pairs in the order specified in Step 1. Then concatenate the pairs with ampersands \(&\) to create the canonicalized query string.

## Step 2: Create a string-to-sign

1.  Calculate the hash-based message authentication code \(HMAC\) value, as defined in [RFC 2104](http://www.ietf.org/rfc/rfc2104.txt). Use the Secure Hash Algorithm 1 \(SHA-1\) algorithm to calculate the HMAC value.

    Add an ampersand \(&\) after the AccessKey secret as the key to calculate the HMAC value. In this example, the key is `testsecret&`.

    ```
    CT9X0VtwR86fNWSnsc6v8YGOjuE=
    ```

    **Note:** When you calculate the signature, the key value specified by RFC 2104 is your `AccessKeySecret` with an ampersand \(`&`\) which has an ASCII value of 38.

2.  Encode the `Signature` parameter based on [RFC 3986](http://tools.ietf.org/html/rfc3986) and add it to the canonicalized query string.

    ```
    http://slb.aliyuncs.com/?Action=DescribeLoadBalancers
    &TimeStamp=2016-02-23T12:46:24Z
    &Format=XML
    &AccessKeyId=testid
    &SignatureMethod=HMAC-SHA1
    &SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf
    &Version=2014-05-26
    &SignatureVersion=1.0
    &Signature=CT9X0VtwR86fNWSnsc6v8YGOjuE%3D
    ```

