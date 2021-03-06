# 性能保障型实例FAQ

负载均衡性能保障型实例提供了可保障的性能指标，阿里云负载均衡计划将于2018年04月01日开始针对性能保障型实例收取规格费。

本文包含以下常见问题：

-   [\#section\_lht\_gym\_vdb](#section_lht_gym_vdb)
-   [\#section\_eth\_yzm\_vdb](#section_eth_yzm_vdb)
-   [\#section\_n5z\_s1n\_vdb](#section_n5z_s1n_vdb)
-   [\#section\_ifx\_kcn\_vdb](#section_ifx_kcn_vdb)
-   [\#p7](#p7)
-   [\#section\_gvt\_kfn\_vdb](#section_gvt_kfn_vdb)
-   [\#section\_hxl\_pfn\_vdb](#section_hxl_pfn_vdb)
-   [\#section\_ehc\_vfn\_vdb](#section_ehc_vfn_vdb)
-   [\#section\_flq\_wfn\_vdb](#section_flq_wfn_vdb)
-   [\#section\_nfy\_xfn\_vdb](#section_nfy_xfn_vdb)
-   [\#section\_wvo\_8kk\_3m9](#section_wvo_8kk_3m9)

## 1什么是负载均衡性能保障型实例？

负载均衡性能保障型实例提供了可保障的性能指标。与之相对的是负载均衡性能共享型实例，资源是所有实例共享的，所以不保障实例的性能指标。

在推出负载均衡性能保障型实例之前，您所有购买的实例均为性能共享型实例。在控制台上，您可以查看已购实例的类型。

性能共享型实例与性能保障型实例区别如下：

|特性|性能共享型实例|性能保障型实例|
|--|-------|-------|
|资源分配|资源共享|资源独享|
|可用性SLA|不提供|99.95%|
|IPv6|×|√|
|支持SNI多证书|×|√|
|支持黑白名单|×|√|
|支持挂ENI|×|√|
|添加ECS弹性网卡辅助IP|×|√|
|HTTP重定向HTTPS|×|√|
|一致性HASH|×|√|
|TLS安全策略|×|√|
|HTTP2|×|√|
|Websocket\(S\)|×|√|

把鼠标移至性能保障型实例的问号图标，可查看具体的性能指标，如下图所示。

![性能保障型实例性能指标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7167559951/p7175.png)

性能保障型实例的三个关键指标如下：

-   最大连接数-Max Connection

    最大连接数定义了一个负载均衡实例能够承载的最大连接数量。当实例上的连接超过规格定义的最大连接数时，新建连接请求将被丢弃。

-   每秒新建连接数-Connection Per Second（CPS）

    每秒新建连接数定义了新建连接的速率。当新建连接的速率超过规格定义的每秒新建连接数时，新建连接请求将被丢弃。

-   每秒查询数-Query Per Second（QPS）

    每秒请求数是七层监听特有的概念，指的是每秒可以完成的HTTP/HTTPS的查询（请求）的数量。当请求速率超过规格所定义的每秒查询数时，新建连接请求将被丢弃。


阿里云负载均衡性能保障型实例开放了如下六种实例规格（各地域因资源情况不同，开放的规格可能略有差异，请以控制台购买页为准）。

|规格|规格|最大连接数|每秒新建连接数（CPS）|每秒查询数（QPS）|购买方式|
|:-|:-|:----|:-----------|:---------|----|
|规格1|简约型I（slb.s1.small）|5,000|3,000|1,000|官网售卖|
|规格2|标准型I（slb.s2.small）|50,000|5,000|5,000|官网售卖|
|规格3|标准型II（slb.s2.medium）|100,000|10,000|10,000|官网售卖|
|规格4|高阶型I（slb.s3.small）|200,000|20,000|20,000|官网售卖|
|规格5|高阶型II（slb.s3.medium）|500,000|50,000|30,000|官网售卖|
|规格6|超强型I（slb.s3.large）|1,000,000|100,000|50,000|官网售卖|
|规格7|超强型II（slb.s3.xlarge）|2,000,000|200,000|100,000|请联系您的客户经理申请|
|规格8|超强型III（slb.s3.xxlarge）|5,000,000|500,000|100,000|请联系您的客户经理申请|

## 2. 性能保障型实例如何收费？

负载均衡性能保障型实例需要收取规格费用，收费模型如下：

性能保障型费用=实例费+流量/带宽费+规格费

**说明：** 负载均衡私网实例也可以选择性能共享型实例或性能保障型实例，性能保障型私网实例，也需要收取规格费用，收费方式与公网性能保障型实例一致，但不收取流量费/带宽费和实例费。

性能保障型实例规格费按使用量收取，即不论您选择的何种规格，实例规格费均会按照您实际使用的规格收取。

例如，您选择了超强型I（slb.s3.large）规格（最大连接数1,000,000；CPS 500,000；QPS 50,000）。您的实例在某个小时内各项指标产生的实际峰值如下：

|最大连接数|每秒新建连接数（CPS）|每秒查询数 （QPS）|
|:----|:-----------|:----------|
|90000|4000|11000|

-   从最大连接数维度看，90,000超过slb.s2.small规格中最大连接数50,000的上限，但未达到slb.s2.medium规格中最大连接数的100,000上限，因此从最大连接数维度计算，该小时规格为slb.s2.medium。
-   从每秒新建连接数（CPS）维度看，4,000超过slb.s1.small规格中CPS 3,000的上限，但未到达slb.s2.small规格中CPS 5,000的上限，因此从CPS维度计算，该小时规格为slb.s2.small。
-   从每秒查询数（QPS）维度看，11,000超过slb.s2.medium规格中QPS 10,000的上限，但未达到slb.s3.small中QPS 20,000的上限，因此从QPS维度计算，该小时规格为slb.s3.small。

    综合以上三个维度，QPS指标的规格（slb.s3.small）最大，因此将QPS维度的规格作为该小时实例的综合规格，该小时内该实例将按照slb.s3.small规格进行计费。


以后每小时规格费均按照上述方式计算，如下图所示：

![每小时规格费计算-2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7167559951/p2301.png)

因此，按量付费的性能保障型实例具有自动弹性伸缩（或计费）的能力。您在购买时所选的规格，是性能的上限，例如您选择高阶型II（slb.s3.medium），那么意味着，您的实例最大可以达到的规格上限就是高阶型I（slb.s3.medium）。

## 3. 性能保障型实例规格费的定价

下表中所列的只是规格费用。除规格费以外，负载均衡实例的实例费和流量正常收取。更多详细信息，请参见[t13419.md\#](/intl.zh-CN/产品定价/按量计费.md)。

|地域|规格|最大连接数|每秒新建连接数（CPS）|每秒查询数（QPS）|规格费（美元/小时）|带宽|
|:-|:-|:----|:-----------|:---------|:---------|--|
|中国内地|规格1：简约型I（slb.s1.small）|5000|3000|1000|限时免费|带宽与规格无关：-   按流量计费实例：实例带宽参见[t15672.md\#](/intl.zh-CN/用户指南/产品限制/带宽峰值限制.md)
-   按带宽计费实例：购买时选择的带宽 |
|规格2：标准型I（slb.s2.small）|50,000|5,000|5,000|0.05|
|规格3：标准型II（slb.s2.medium）|100,000|10,000|10,000|0.10|
|规格4：高阶型I（slb.s3.small）|200,000|20,000|20,000|0.20|
|规格5：高阶型I（slb.s3.medium）|500,000|50,000|30,000|0.31|
|规格6：超强型I（slb.s3.large）|1,000,000|100,000|50,000|0.51|
|海外和中国香港|规格1：简约型I（slb.s1.small）|5,000|3,000|1,000|限时免费|带宽与规格无关-   按流量计费实例：实例带宽参见[t15672.md\#](/intl.zh-CN/用户指南/产品限制/带宽峰值限制.md)
-   按带宽计费实例：购买时选择的带宽 |
|规格2：标准型I（slb.s2.small）|50,000|5,000|5,000|0.06|
|规格3：标准型II（slb.s2.medium）|100,000|10,000|10,000|0.12|
|规格4：高阶型I（slb.s3.small）|200,000|20,000|20,000|0.24|
|规格5：高阶型II（slb.s3.large）|500,000|50,000|30,000|0.37|
|规格6：超强型I（slb.s3.large）|1,000,000|100,000|50,000|0.61|

## 4. 如何选择性能保障型实例？

规格费是按量（弹性）计费的，因此建议您直接选择您可以买到的最大规格，对于大多数用户而言，即高阶型I（slb.s3.large），这样可以保证较好的业务灵活性（弹性），且不会让您额外多付出成本。但如果您认为您的业务量不太可能到达超强型I（slb.s3.large），也可以设置一个合理的弹性上限，例如高阶型II（slb.s3.medium）。

## 5. 是否可以调整性能保障型实例的规格？

您可在控制台对性能保障型实例进行变配。详细信息，请参见[t15648.md\#]()。

**说明：**

-   将性能共享型实例变更为性能保障型实例后，无法再将其变更回性能共享型。
-   由于历史存量原因，部分实例可能存在于较老的集群。此部分实例在变配到性能保障型实例时，因为需要将实例迁移，因此可能出现10~30秒的业务中断，其他变配操作均不会影响业务。因此建议在业务低谷期进行此类变配。
-   所有的变配操作都不影响负载均衡实例的IP地址。

![警告信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8167559951/p7345.png)

## 6. 性能保障型实例何时收费？

阿里云负载均衡于2018年04月01日开始针对性能保障型实例收取规格费，同时继续保留性能共享型实例的售卖。

性能保障型实例的规格费收取将按地域分批次生效：

-   第一批：

    生效时间：04月01日至04月10日陆续生效

    生效地域：新加坡、马来西亚（吉隆坡）、印度尼西亚（雅加达）、印度（孟买）、美国（硅谷）和美国（弗吉尼亚）

-   第二批：

    生效时间：04月11日至04月20日陆续生效

    生效地域：华东1（杭州）、华北3（张家口）、华北5（呼和浩特）和中国香港

-   第三批：

    生效时间：04月21日至04月30日陆续生效

    生效地域：华北1（青岛）、华北2（北京）、华东2（上海）和华南1（深圳）


## 7. 收取规格费以后，性能共享型实例会额外收取费用吗？

不会。

原有的性能共享型实例（如果您不将其变配性能保障型）将继续保持为性能共享型实例，不收取规格费。您也可以通过变配，将性能共享型实例升级成性能保障型实例。变更成性能保障型后，当性能保障型实例开始正式收费时，该实例将收取规格费。

## 8. 为何有时性能保障型实例看起来达不到规格中的性能指标上限？

短木板原理。

性能保障型实例并不保障三个指标（包含带宽指标）同时达到指定规格的指标上限。即规格中哪个指标先达到峰值，就以哪个指标开始限速。

例如某用户选择高阶型I（slb.s3.small）实例，当实例的QPS已经达到20000，但并发连接数确远未达到20万，那么该实例最大连接数可能永远都不会达到规格上限，因为新建的连接请求会因为QPS达到上限而被丢弃。

## 9. 还可以购买性能共享型实例吗？

不可以。

## 10. 私网负载均衡实例也会收取规格费吗？

如果您选择的是性能共享型私网实例，则不会收取规格费。如果您选择的是性能保障型私网实例，则需要收取规格费。

规格费收取方式与公网实例规格费计费规则一致。私网实例免收实例费和流量费。

## 11.性能保障型实例不够用了怎么办？

当您需要更多实例配额，且配额管理中已不能申请更高时，可以考虑申请拥有更多保障型规格实例Quota的特权，配额编码slb\_privilege\_allow\_more\_guaranteed\_performance\_instances，申请此特权后，即可保有更多保障型实例配额，但无法保有更多共享型实例，具体操作，请参见[t120245.md\#](/intl.zh-CN/用户指南/产品限制/配额管理.md)。

