# Forward requests from the same domain name but different URLs

SLB supports Domain name- and URL-based forwarding rules. You can forward requests from the same domain name but different URLs to separate backend servers. This allows you to optimize load balancing among your server resources.

**Note:** You can configure forwarding rules only for Layer-7 listeners that use HTTPS or HTTP.

Four ECSs deployed with NGINX servers are used to demonstrate how to configure forwarding rules specified by domain name and URL. The following table lists the forwarding requirements.

|Frontend request|Forwarded to|
|:---------------|:-----------|
|www.aaa.com/tom|Backend servers SLB\_tom1 and SBL\_tom2, which belong to the TOM VServer group|
|www.aaa.com/jerry|The backend servers SLB\_jerry1 and SBL\_jerry2 belong to the VServer group JERRY|

## Domain name- and URL-based forwarding rules

You can configure domain name-based or URL-based forwarding rules for an SLB instance that has Layer-7 listeners to distribute requests from different domain names or URLs to different ECS instances.

URL-based forwarding rules support string matching and the rule with the longest matched prefix is applied. For example, if the two forwarding rules /abc and /abcd are created and a request with the prefix of /abcde is received, the rule /abcd is applied.

Domain name-based forwarding rules include exact matching and wildcard matching.

-   Exact domain name: www.aliyun.com
-   Wildcard domain name: \*.aliyun.com and \*.market.aliyun.com

    When a request matches multiple forwarding rules, exact matching prevails over wildcard matching, and exact wildcard matching prevails over less exact wildcard matching. The following table shows the priority of Domain name-based forwarding rules.

    |Type|Request URL|Domain name-based forwarding rule|
|www.aliyun.com|\*.aliyun.com|\*.market.aliyun.com|
    |:---|:----------|:--------------------------------|
    |:-------------|:------------|:-------------------|
    |Exact matching|www.aliyun.com|✓|×|×|
    |Exact wildcard matching|market.aliyun.com|×|✓|×|
    |Less exact wildcard matching|info.market.aliyun.com|×|×|✓|


You can add multiple forwarding rules to a listener. Each forwarding rule is associated with a VServer group. A VServer group consists of multiple ECS instances. For example, you can configure a listener to forward read requests to one VServer group and write requests to another VServer group. This allows you to optimize load balancing among your server resources.

After you configure forwarding rules, SLB applies the rules to distribute traffic based on the following models:

-   Requests that contain domain names are forwarded based on domain name-based forwarding rules.
    -   Model 1: If a forwarding rule matches the domain name, the system continues to match the URL.

        If the URL is matched, requests are forwarded to the specified VServer group. If no forwarding rule matches the URL, the requests are forwarded based only on root domain-based forwarding rules that contain only domain names.

        If you do not add root domain-based forwarding rules, the error message 404 is returned to the client.

    -   If no forwarding rule matches the domain name, requests are forwarded in Model 2.
-   Model 2: If the requests do not contain domain names or no forwarding rule matches the domain name, requests are forwarded based on URL-based forwarding rules that contain only URLs.

    If a forwarding rule is matched, requests are forwarded to the VServer group. If no forwarding rule is matched, requests are forwarded to the default VServer group.


![Forwarding rules](../images/p102737.png)

## Add URL-based forwarding rules

Before you add URL-based forwarding rules to a listener, make sure that the following requirements are met:

1.  An Internet SLB instance is created. For more information, see [Create an SLB instance](/intl.en-US/Classic Load Balancer/User Guide/Instance/Create an SLB instance.md).
2.  A Layer-7 listener is created. The scheduling algorithm is Round-Robin. For more information, see [Add an HTTP listener](/intl.en-US/Classic Load Balancer/User Guide/Listeners/Add an HTTP listener.md) or [Add an HTTPS listener](/intl.en-US/Classic Load Balancer/User Guide/Listeners/Add an HTTPS listener.md).
3.  Two VServer groups TOM and JERRY are created. For more information, see [Add ECS instances to a VServer group](/intl.en-US/Classic Load Balancer/User Guide/Backend servers/VServer groups/Add ECS instances to a VServer group.md).
    -   Servers SLB\_tom1 and SBL\_tom2 are added to the VServer group TOM. The port is set to 80 and the default weight value 100 is used.
    -   Servers SLB\_jerry1 and SLB\_jerry2 are added to the VServer group JERRY. The port is set to 80 and the default weight value 100 is used.

Perform the following operations:

1.  Log on to the [Server Load Balancer console](https://slb.console.aliyun.com/slb/).

2.  In the top navigation bar, select the region where the SLB instance is deployed.

3.  On the Instances page, click the ID of the SLB instance.

4.  On the Listener tab, find the Layer-7 listener and click **Set Forwarding Rule** in the **Actions** column.

5.  Configure two forwarding rules: forward requests from the www.aaa.com/tom to the TOM VServer group and requests from the www.aaa.com/jerry to the JERRY VServer group.

    ![Configure forwarding rules](../images/p86443.png)

    Configure the following parameters:

    -   **Domain Name**: Enter the domain name to which requests are forwarded. The domain name can only contain letters, digits, hyphens \(-\), and periods \(.\).
    -   **URL**: Enter the URL to which requests are forwarded. The path must start with a forward slash \(/\), and can only contain letters, numbers, and special characters. Special characters include

        -. /%? \#&

        **Note:** If you only want to configure a URL-based forwarding rule, leave Domain Name empty.

    -   **VServer Group**: Select the VServer Group to be associated with the forwarding rule.
    -   **Description**: Enter a description.
    **Note:** For more information about the maximum number of forwarding rules that can be specified for an HTTP or HTTPS listener, see [Limits](/intl.en-US/Classic Load Balancer/User Guide/Limits/Limits.md).

6.  Click **Add Forwarding Rules**.

7.  Click **OK**.

8.  Test whether the forwarding rules are configured.

    -   Enter www.aaa.com/jerry in the browser and the following result is returned.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/4172/15382791923185_en-US.png)

    -   Enter www.aaa.com/tom in the browser and the following result is returned.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/4172/15382791923186_en-US.png)

    -   Enter www.aaa.com in the browser and the following result is returned.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/4172/15382791923187_en-US.png)

