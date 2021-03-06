# DescribeLoadBalancers {#doc_api_879503 .reference}

You can call the DescribeLoadBalancers API to query the created SLB instances.

## Debug {#apiExplorer .section}

Click [here](https://api.aliyun.com/#product=Slb&api=DescribeLoadBalancers) to perform a debug operation in OpenAPI Explorer and automatically generate an SDK code example.

## Request parameters {#parameters .section}

|Name|Type|Required?|Example value|Description|
|----|----|---------|-------------|-----------|
|Action|String|Yes|DescribeLoadBalancers|The action to perform. Valid value: **DescribeLoadBalancers**

 |
|RegionId|String|Yes|cn-hangzhou|The region to which the SLB instance belongs.

 You can query the region ID by referring to the list of [regions and zones](~~40654~~) or by calling the [DescribeRegions](~~25609~~) API.

 |
|Address|String|No|192.168.0.6|The IP address of the SLB instance

 |
|AddressIPVersion|String|No|ipv4|The IP version, which can be set to ipv4 or ipv6.

 **Note:** Currently, only Zone E and Zone F in the China \(Hangzhou\) region, and Zone F and Zone G in the China \(Beijing\) region are supported by ipv6 instances and the instances must be guaranteed-performance instances.

 |
|AddressType|String|No|intranet|The network type of the SLB instances. Valid values: **intranet** or **internet**.

 |
|InternetChargeType|String|No|paybybandwidth|The billing method of Internet SLB instances. Valid values: **paybybandwidth | paybytraffic**

 |
|LoadBalancerId|String|No|lb-bp1b6c719dfa08exfuca5|The ID of the SLB instance.

 You can enter up to 10 IDs. Multiple IDs must be separated by commas.

 |
|LoadBalancerName|String|No|abc1|The name of the SLB instance.

 You can enter up to 10 names. Multiple names must be separated by commas.

 |
|LoadBalancerStatus|String|No|active|The status of the SLB instance.

 -   inactive: When an SLB instance is inactive, the listeners of the instance do not distribute traffic.
-   active: After an instance is created, it is in active status by default.
-   locked: The SLB instance is locked.

 |
|MasterZoneId|String|No|cn-hangzhou-b|The primary zone ID of the SLB instance

 |
|NetworkType|String|No|vpc|The network type of intranet SLB instances. Valid values: **vpc | classic**.

 -   vpc: a VPC-type network
-   classic: a classic network

 |
|PageNumber|Integer|No|1|The page number in the case of paging query

 |
|PageSize|Integer|No|50|The maximum number of entries on a page

 |
|PayType|String|No|PayOnDemand|The billing method of SLB instances. Valid values: **PayOnDemand | PrePay**

 |
|ResourceGroupId|String|No|rg-acfmxazb4ph6aiy|The ID of the enterprise resource group

 |
|ServerId|String|No|vm-231|The ID of the added backend server \(ECS instance\)

 |
|ServerIntranetAddress|String|No|10.80.102.20|The intranet address of the added backend server \(ECS instance\).

 You can enter multiple values, and each value must be separated by a comma.

 |
|SlaveZoneId|String|No|cn-hangzhou-d|The backup zone ID of the SLB instance.

 Currently, the multi-zone feature is not supported for users of Alibaba Cloud???s financial service solutions.

 |
|Tags|String|No|\{"tagKey":"Key1","tagValue":"Value1"\}|The tag list bound to the SLB instance. It is a JSON formatted list and contains TagKey and TagValue pairs.

 For each request, the list can contain up to 10 tags.

 |
|VSwitchId|String|No|vsw-bp12mw1f8k3jgygk9bmlj|The ID of the VSwitch to which the SLB instance belongs

 |
|VpcId|String|No|vpc-bp1aevy8sofi8mh1qc5cm|The ID of the VPC where the SLB instance is created

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example value|Description|
|----|----|-------------|-----------|
|LoadBalancers|??|??|Array format. A list of SLB instances is returned, as described in the following table.

 |
|???LoadBalancerId|String|282b00102ac-cn-east-hangzhou-01|The ID of the SLB instance

 |
|???LoadBalancerName|String|def|The name of the SLB instance

 |
|???LoadBalancerStatus|String|active|The status of the SLB instance.

 -   inactive: When an SLB instance is inactive, the listeners of the instance do not distribute traffic.
-   active: After an instance is created, it is in active status by default.
-   locked: The SLB instance is locked.

 |
|???Address|String|100.98.28.55|The IP address of the SLB instance

 |
|???RegionId|String|cn-hangzhou|The ID of the region to which the SLB instance belongs

 |
|???RegionIdAlias|String|cn-hangzhou|The alias of the region to which the SLB instance belongs

 |
|???AddressType|String|intranet|The network type of the SLB instance

 |
|???VSwitchId|String|vsw-255ecrwq5|The ID of the VSwitch to which the intranet SLB instance belongs

 |
|???VpcId|String|vpc-25dvzy9f8|The ID of the VPC where the intranet SLB instance is created

 |
|???NetworkType|String|vpc|The network type of the intranet SLB instance. Valid values:

 -   vpc: a VPC-type network
-   classic: a classic network

 |
|???CreateTime|String|2017-08-31T02:49:05Z|The time when the SLB instance is created

 |
|???MasterZoneId|String|cn-hangzhou-b|The ID of the primary zone

 |
|???SlaveZoneId|String|cn-hangzhou-d|The ID of the backup zone

 |
|???AddressIPVersion|String|ipv4|The IP version, which can be set to ipv4 or ipv6.

 |
|???CreateTimeStamp|Long|1504147745000|The timestamp at which the SLB instance is created

 |
|???InternetChargeType|String|paybybandwidth|The billing method of an Internet SLB instance. Valid values:

 -   paybytraffic: billed by traffic \(default value\)

 **Note:** If the value of PayType is PrePay, only bandwidth-based billing is supported.

 |
|???PayType|String|PrePay|The billing method of SLB instances. Valid values: PayOnDemand or PrePay.

 |
|???ResourceGroupId|String|rg-atstuj3rtoptyui|The ID of the enterprise resource group

 |
|PageNumber|Integer|1|The page number of the SLB instance list

 |
|PageSize|Integer|50|The number of entries on the current page

 |
|RequestId|String|365F4154-92F6-4AE4-92F8-7FF34B540710|The ID of the request

 |
|TotalCount|Integer|1|The total number of instances that meet the filter conditions

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://[Endpoint]/? Action=DescribeLoadBalancers
&RegionId=cn-hangzhou
&<CommonParameters>

```

Normal response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeLoadBalancersResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>50</PageSize>
  <LoadBalancers>
    <LoadBalancer>
      <CreateTimeStamp>1541679713000</CreateTimeStamp>
      <LoadBalancerName>abc1</LoadBalancerName>
      <RegionIdAlias>cn-hangzhou</RegionIdAlias>
      <ResourceGroupId>rg-acfmxazb4ph6aiy</ResourceGroupId>
      <AddressIPVersion>ipv4</AddressIPVersion>
      <LoadBalancerId>lb-bp1b6c719dfa08exfuca5</LoadBalancerId>
      <VSwitchId>vsw-bp12mw1f8k3jgygk9bmlj</VSwitchId>
      <InternetChargeType>4</InternetChargeType>
      <VpcId>vpc-bp1aevy8sofi8mh1qc5cm</VpcId>
      <SlaveZoneId>cn-hangzhou-d</SlaveZoneId>
      <NetworkType>vpc</NetworkType>
      <MasterZoneId>cn-hangzhou-b</MasterZoneId>
      <CreateTime>2018-11-08T20:21Z</CreateTime>
      <Address>192.168.0.6</Address>
      <RegionId>cn-hangzhou</RegionId>
      <AddressType>intranet</AddressType>
      <PayType>PayOnDemand</PayType>
      <LoadBalancerStatus>active</LoadBalancerStatus>
    </LoadBalancer>
  </LoadBalancers>
  <RequestId>1C7445CB-C21C-4C19-9A3C-65C3190D1944</RequestId>
</DescribeLoadBalancersResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":50,
	"RequestId":"1C7445CB-C21C-4C19-9A3C-65C3190D1944",
	"LoadBalancers":{
		"LoadBalancer":[
			{
				"CreateTimeStamp":1541679713000,
				"LoadBalancerName":"abc1",
				"RegionIdAlias":"cn-hangzhou",
				"ResourceGroupId":"rg-acfmxazb4ph6aiy",
				"AddressIPVersion":"ipv4",
				"LoadBalancerId":"lb-bp1b6c719dfa08exfuca5",
				"VSwitchId":"vsw-bp12mw1f8k3jgygk9bmlj",
				"InternetChargeType":"4",
				"VpcId":"vpc-bp1aevy8sofi8mh1qc5cm",
				"SlaveZoneId":"cn-hangzhou-d",
				"NetworkType":"vpc",
				"MasterZoneId":"cn-hangzhou-b",
				"RegionId":"cn-hangzhou",
				"Address":"192.168.0.6",
				"CreateTime":"2018-11-08T20:21Z",
				"AddressType":"intranet",
				"PayType":"PayOnDemand",
				"LoadBalancerStatus":"active"
			}
		]
	}
}
```

## Error codes { .section}

[Click here to view the error codes.](https://error-center.aliyun.com/status/product/Slb)

