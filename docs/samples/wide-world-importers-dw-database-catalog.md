---
title: WideWorldImporters OLAP 数据库目录-SQL |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 8039efbdb9157b45f8fcc67d0b8f72d367d81e52
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2018
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW 数据库目录
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
架构、 表和 WideWorldImportersDW 数据库中的存储的过程的说明。 

WideWorldImportersDW 数据库用于数据仓库和分析处理。 在 WideWorldImporters 数据库中，生成有关销售和购买的事务数据并将其加载到 WideWorldImportersDW 数据库使用**每日 ETL 过程**。

WideWorldImportersDW 中的数据，因此镜像 WideWorldImporters 中的数据，但以不同的方式来组织引用表。 尽管 WideWorldImporters 有传统规范化的架构，但是，使用 WideWorldImportersDW[星型架构](https://wikipedia.org/wiki/Star_schema)其表设计的方法。 除了事实数据表和维度表中，数据库在 ETL 过程中包括大量使用的临时表。

## <a name="schemas"></a>架构

三个架构进行组织的不同类型的表。

|架构|Description|
|-----------------------------|---------------------|
|维度|维度表。|
|事实|事实数据表。|  
|集成|临时表和所需的 ETL 其他对象。|  

## <a name="tables"></a>表

下面列出了维度和事实数据表。 集成架构中的表仅用于 ETL 过程中，且未列。

### <a name="dimension-tables"></a>维度表

WideWorldImportersDW 具有以下维度表。 说明内容包括 WideWorldImporters 数据库中源表的关系。

|表|源表|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|日期|包含有关日期，包括财务年度的信息的新表 (基于年 11 月 1 日开始财务年)。|
|Employee|`Application.People`中创建已分区表或索引。|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|供应商|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`中创建已分区表或索引。|
|TransactionType|`Application.TransactionTypes`中创建已分区表或索引。|

### <a name="fact-tables"></a>事实数据表

WideWorldImportersDW 具有以下事实数据表。 说明内容包括在 WideWorldImporters 数据库，以及每个事实数据表通常用于/报告分析的查询的类与源表之间的关系。

|表|源表|示例分析|
|-----------------------------|---------------------|---------------------|
|订单|`Sales.Orders` 和 `Sales.OrderLines`|销售人员，选取器/打包程序工作效率，以及上的时间选取订单。 此外，较低的常用的情况下导致回订单。|
|销售点|`Sales.Invoices` 和 `Sales.InvoiceLines`|销售日期、 传递日期、 随时间推移的盈利率、 按销售人员列出收益率。|
|购买|`Purchasing.PurchaseOrderLines`|预期的 vs 实际前置时间|
|事务|`Sales.CustomerTransactions` 和 `Purchasing.SupplierTransactions`|测量问题日期 vs 终止日期和金额。|
|移动|`Warehouse.StockTransactions`|随着时间的推移动作数。|
|股票控股|`Warehouse.StockItemHoldings`|有关现有库存级别和值。|

## <a name="stored-procedures"></a>存储过程

存储的过程用于主要 ETL 过程以及进行配置。

任何扩展示例还鼓励使用`Reports`Reporting Services 报表的架构和`PowerBI`Power BI 访问权限的架构。

### <a name="application-schema"></a>应用程序架构

使用这些过程来配置示例。 它们用于将企业版功能应用于此示例中，标准版版本添加 PolyBase，和重设种子 ETL。

|过程|用途|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|将应用事实表的分区和列存储索引。|
|Configuration_ConfigureForEnterpriseEdition|将应用分区，列存储索引和内存中。|
|Configuration_EnableInMemory|集成临时表替换为 SCHEMA_ONLY 的内存优化表，以提高 ETL 性能。|
|Configuration_ApplyPolybase|配置外部数据源、 文件格式和表。|
|Configuration_PopulateLargeSaleTable|应用 enterprise 版本更改，然后为作为其他历史记录 2012年日历年填充的数据量很大。|
|Configuration_ReseedETL|删除现有的数据，并重新启动 ETL 种子。 这使得重新填充 OLAP 数据库以匹配在 OLTP 数据库中的更新的行。|

### <a name="integration-schema"></a>集成架构

在 ETL 过程中使用的过程划分这些类别中：
- ETL 包的所有 Get * 过程的帮助器过程。
- ETL 包用于迁移的过程 DW 表的所有迁移 * 过程暂存数据。
- `PopulateDateDimensionForYear` -采用每一年，并确保在中进行填充该年度的所有日期`Dimension.Date`表。

### <a name="sequences-schema"></a>序列架构

若要配置数据库中的序列的过程。

|过程|用途|
|-----------------------------|---------------------|
|ReseedAllSequences|调用过程`ReseedSequenceBeyondTableValue`所有序列。|
|ReseedSequenceBeyondTableValue|用于在使用相同的序列任何表中重新定位到值之外的下一步序列值。 (如`DBCC CHECKIDENT`为标识列等效序列但跨可能多个表。)|
