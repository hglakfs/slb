# CreateLoadBalancer {#doc_api_876110 .reference}

You can call the CreateLoadBalancer API to create an SLB instance.

Before you call this API, note the following:

-   After the instance is created, fees are incurred. For more information, see [Billing method](~~27692~~).
-   If you do not specify the instance specification \(**LoadBalancerSpec**\), a shared-performance instance is created. Therefore, we recommend that you call the **LoadBalancerSpec** API to specify the instance specification when creating an SLB instance.

## Debug {#apiExplorer .section}

Click [here](https://api.aliyun.com/#product=Slb&api=CreateLoadBalancer) to perform a debug operation in OpenAPI Explorer and automatically generate an SDK code example.

## Request parameters {#parameters .section}

|Name|Type|Required?|Example value|Description|
|----|----|---------|-------------|-----------|
|Action|String|Yes|CreateLoadBalancer|The action to perform. Valid value: **CreateLoadBalancer**

 |
|RegionId|String|Yes|cn-hangzhou|The region to which the SLB instance belongs.

 You can query the region ID by calling the [DescribeRegions](~~25609~~) API.

 |
|Address|String|No|192.168.0.1|Specify the IP address of the private network for the SLB instance, which must be in the destination CIDR block of the corresponding switch.

 |
|AddressIPVersion|String|No|ipv4|The IP version of the SLB instance, which can be set to ipv4 or ipv6.

 |
|AddressType|String|No|internet|The network type of the SLB instance. Valid values:

 -   **internet**: After an Internet SLB instance is created, the system allocates a public IP address so that the instance can forward requests from the Internet.
-   **intranet**: After an intranet SLB instance is created, the system allocates an intranet IP address so that the instance can only forward intranet requests.

 |
|AutoPay|Boolean|No|true|Whether to automatically pay the bill for a Subscription Internet instance.

 Valid values: **true | false \(default value\)**.

 **Note:** This parameter applies only to the China site.

 |
|Bandwidth|Integer|No|10|The peak bandwidth of the listener.

 |
|ClientToken|String|No|5A2CFF0E-5718-45B5-9D4D-70B3FF3898|Guarantee the idempotence of the request. The value is generated by a client. It must be unique among all requests and can contain a maximum of 64 ASCII characters.

 |
|Duration|Integer|No|1|The subscription duration of a Subscription Internet instance. Valid values:

 -   If **PricingCycle** is **month**, valid values are **1???9**.
-   If**PricingCycle**is **year**, valid values are**1???3**.

 **Note:** This parameter applies only to the China site.

 |
|InternetChargeType|String|No|paybytraffic|The billing method of an Internet instance. Valid values:

 -   paybytraffic: billed by the traffic \(default value\)

 |
|LoadBalancerName|String|No|abc|The name of the SLB instance.

 The name must be 2 to 128 characters in length, must start with Chinese characters or English letters, and can contain numbers, underscores \(\_\), periods \(.\), and hyphens \(-\).

 When this parameter is not specified, a default instance name is assigned by the system.

 |
|LoadBalancerSpec|String|No|slb.s2.small|The specification of the SLB instance. Valid values:

 -   slb.s1.small
-   slb.s2.small
-   slb.s2.medium
-   slb.s3.small
-   slb.s3.medium
-   slb.s3.large

The available specifications vary by region.

 Currently, the following regions are supported by guaranteed-performance instances: China North 1 \(Qingdao\), China North 2 \(Beijing\), China East 1 \(Hangzhou\), China East 2 \(Shanghai\), China South 1 \(Shenzhen\), China North 3 \(zhangjiakou\), China North 5 \(Hohhot\), Asia Pacific SE 1 \(Singapore\), UK \(London\), EU Central 1 \(Frankfurt\), Asia Pacific SE 2 \(Sydney\), Asia Pacific SE 3 \(Kuala Lumpur\), Middle East 1 \(Dubai\), Asia Pacific SE 5 \(Jakarta\), US West 1 \(Silicon Valley\), Asia Pacific SOU 1 \(Mumbai\), Asia Pacific NE 1 \(Tokyo\), Hong Kong, and US East 1 \(Virginia\). For more information, see [Guaranteed-performance instance](~~27657~~).

 **Note:** If you do not configure the specification of the instance, a shared-performance instance is created.

 |
|MasterZoneId|String|No|cn-hangzhou-b|The primary zone ID of the SLB instance.

 You can query the primary and standby zones in a region by calling the [DescribeZone](~~27585~~) API.

 |
|PayType|String|No|PayOnDemand|The billing method of the instance. Valid values:

 -   **PayOnDemand**: Pay-As-You-Go

 |
|PricingCycle|String|No|month|The subscription duration of a Subscription Internet instance. Valid values: **month | year**.

 **Note:** This parameter applies only to the China site.

 |
|ResourceGroupId|String|No|rg-atstuj3rtoptyui|The ID of the enterprise resource group.

 |
|SlaveZoneId|String|No|cn-hangzhou-d|The standby zone ID of the SLB instance.

 You can query the primary and standby zones in a region by calling the [DescribeZone](~~27585~~) API.

 |
|VSwitchId|String|No|vsw-bp12mw1f8k3jgygk9bmlj|The ID of the VSwitch to which the SLB instance belongs.

 This parameter must be specified if you want to create an intranet instance. If this parameter is specified, the value of the **AddessType** parameter is set to **intranet** by default.

 |
|VpcId|String|No|vpc-bp1aevy8sofi8mh1qc5cm|The ID of the VPC to which the SLB instance belongs.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example value|Description|
|----|----|-------------|-----------|
|LoadBalancerId|String|139a00604ad-cn-east-hangzhou-01|The ID of the SLB instance

 |
|Address|String|42.250.6.36|The IP address of the SLB instance

 |
|VpcId|String|vpc-25dvzy9f8|The ID of the VPC to which the SLB instance belongs

 |
|VSwitchId|String|vsw-255ecrwq5|The ID of the VSwitch to which the SLB instance belongs

 |
|LoadBalancerName|String|abc|The name of the SLB instance

 |
|AddressIPVersion|String|ipv4|The IP address type of the SLB instance

 |
|NetworkType|String|classic|The network type of the SLB instance

 |
|OrderId|Long|201429619788910|The ID of the order

 |
|RequestId|String|365F4154-92F6-4AE4-92F8-7FF34B540710|The ID of the request

 |
|ResourceGroupId|String|rg-atstuj3rtoptyui|The ID of the enterprise resource group

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://[Endpoint]/? Action=CreateLoadBalancer
&RegionId=cn-hangzhou
&<CommonParameters>

```

Normal response examples

`XML` format

``` {#xml_return_success_demo}
<CreateLoadBalancerResponse>
  <NetworkType>vpc</NetworkType>
  <LoadBalancerName>abc</LoadBalancerName>
  <Address>192.168.0.6</Address>
  <ResourceGroupId>rg-acfmxazb4ph6aiy</ResourceGroupId>
  <RequestId>AB197CF0-D9E9-4475-A89D-35DBCCF13BBE</RequestId>
  <AddressIPVersion>ipv4</AddressIPVersion>
  <LoadBalancerId>lb-bp1b6c719dfa08exfuca5</LoadBalancerId>
  <VSwitchId>vsw-bp12mw1f8k3jgygk9bmlj</VSwitchId>
  <VpcId>vpc-bp1aevy8sofi8mh1qc5cm</VpcId>
</CreateLoadBalancerResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"NetworkType":"vpc",
	"LoadBalancerName":"abc",
	"RequestId":"AB197CF0-D9E9-4475-A89D-35DBCCF13BBE",
	"ResourceGroupId":"rg-acfmxazb4ph6aiy",
	"Address":"192.168.0.6",
	"AddressIPVersion":"ipv4",
	"LoadBalancerId":"lb-bp1b6c719dfa08exfuca5",
	"VSwitchId":"vsw-bp12mw1f8k3jgygk9bmlj",
	"VpcId":"vpc-bp1aevy8sofi8mh1qc5cm"
}
```

Error response examples

`XML` format

``` {#xml_return_failed_demo}
<CreateLoadBalancerResponse>
  <Code>InvalidParameter</Code>
  <Message>The specified parameter is not valid. </Message>
  <HostId>slb.aliyuncs.com</HostId>
  <RequestId>0669D684-69D8-408E-A4FA-B9011E0F4E66</RequestId>
</CreateLoadBalancerResponse>

```

`JSON` format

``` {#json_return_failed_demo}
{
	"Message":"The specified parameter is not valid.",
	"RequestId":"0669D684-69D8-408E-A4FA-B9011E0F4E66",
	"HostId":"slb.aliyuncs.com",
	"Code":"InvalidParameter"
}
```

## Error codes { .section}

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|Operation.NotAllowed|Operation Denied. The charge type of internet prepay instance can only be paybybandwidth.|The operation is not allowed. An unfinished purchase order exists.|
|400|Operation.NotAllowed|Operation Denied. The charge type of intranet prepay instance can only be paybytraffic.|The operation is not allowed. An unfinished purchase order exists.|
|400|InvalidParameter|Illegal parameter. The IP address is not in subnet.|The parameter Bandwidth is invalid. Please check that the parameter is correct.|

[Click here to view the error codes.](https://error-center.aliyun.com/status/product/Slb)

