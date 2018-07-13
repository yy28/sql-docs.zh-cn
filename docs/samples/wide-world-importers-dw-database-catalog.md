---
title: WideWorldImporters OLAP 数据库目录-SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: de537c60f8adf2d4860e236421dd0457871ea025
ms.sourcegitcommit: 89983916c39b1c3ecf340de6a4febb2ed33129e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36964289"
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW 数据库目录
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
架构、 表和 WideWorldImportersDW 数据库中的存储的过程的说明。 

WideWorldImportersDW 数据库用于数据仓库和分析处理。 在 WideWorldImporters 数据库中，生成有关销售和采购的事务数据并将其加载到 WideWorldImportersDW 数据库使用**日常 ETL 处理过程**。

WideWorldImportersDW 中的数据从而镜像 WideWorldImporters 中的数据，但这些表组织以不同的方式。 尽管 WideWorldImporters 具有传统的规范化的架构，但是，使用 WideWorldImportersDW[星型架构](https://wikipedia.org/wiki/Star_schema)其表设计的方法。 事实数据表和维度表中，除了数据库 ETL 过程中包括所用的临时表的数。

## <a name="schemas"></a>架构

三个架构进行组织不同类型的表。

|架构|Description|
|-----------------------------|---------------------|
|维度|维度表。|
|事实|事实数据表。|  
|集成|临时表和所需的 ETL 其他对象。|  

## <a name="tables"></a>表

下面列出了维度和事实数据表。 集成架构中的表仅用于 ETL 进程，进程和未列出。

### <a name="dimension-tables"></a>维度表

WideWorldImportersDW 具有以下维度表。 说明内容包括 WideWorldImporters 数据库中与源数据表的关系。

|表|源表|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|date|包含有关日期，包括财务年度的信息的新表 (基于 11 月 1 日开始财政年)。|
|Employee|`Application.People`的用户。|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|供应商|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`的用户。|
|TransactionType|`Application.TransactionTypes`的用户。|

### <a name="fact-tables"></a>事实数据表

WideWorldImportersDW 具有以下事实数据表。 说明内容包括在 WideWorldImporters 数据库，以及每个事实数据表通常与一起使用的分析报告的查询的类与源数据表的关系。

|表|源表|示例分析|
|-----------------------------|---------------------|---------------------|
|订单|`Sales.Orders` 和 `Sales.OrderLines`|销售人员选取器/packer 工作效率和上的时间选择订单。 此外，较低的股票的情况下导致要延期交货。|
|销售|`Sales.Invoices` 和 `Sales.InvoiceLines`|销售日期、 交付日期、 随时间推移的盈利能力、 销售人员的盈利率。|
|购买|`Purchasing.PurchaseOrderLines`|预期的与实际前置时间|
|事务|`Sales.CustomerTransactions` 和 `Purchasing.SupplierTransactions`|测量问题日期 vs 终止日期和数量。|
|移动|`Warehouse.StockTransactions`|随着时间的推移的动作。|
|股|`Warehouse.StockItemHoldings`|有关现有库存级别和值。|

## <a name="stored-procedures"></a>存储过程

主要用于 ETL 进程和出于配置目的使用存储的过程。

该示例的任何扩展且建议使用`Reports`Reporting Services 报表的架构和`PowerBI`Power BI 访问权限的架构。

### <a name="application-schema"></a>应用程序架构

使用这些过程来配置示例。 它们用于将企业版功能应用到标准版版本的示例中，添加 PolyBase，和重设种子 ETL。

|过程|用途|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|适用于事实表的分区和列存储索引。|
|Configuration_ConfigureForEnterpriseEdition|将应用分区列存储索引和内存中。|
|Configuration_EnableInMemory|将集成临时表替换为 SCHEMA_ONLY 的内存优化表，以提高 ETL 性能。|
|Configuration_ApplyPolybase|配置外部数据源、 文件格式和表。|
|Configuration_PopulateLargeSaleTable|Enterprise edition 更改应用，然后将更多的数据填充为其他历史记录 2012年日历年。|
|Configuration_ReseedETL|删除现有数据并重新启动 ETL 种子。 这允许重新填充 OLAP 数据库以匹配在 OLTP 数据库中已更新的行。|

### <a name="integration-schema"></a>集成架构

在 ETL 过程中使用的过程分为以下类别：
- ETL 包的所有 Get * 过程的帮助器过程。
- ETL 包用于迁移的过程装载到数据仓库表的所有迁移 * 过程的数据。
- `PopulateDateDimensionForYear` -采用一年，并可确保在中填充该年的所有日期`Dimension.Date`表。

### <a name="sequences-schema"></a>序列架构

若要配置数据库中的序列的过程。

|过程|用途|
|-----------------------------|---------------------|
|ReseedAllSequences|调用过程`ReseedSequenceBeyondTableValue`的所有序列。|
|ReseedSequenceBeyondTableValue|用于在任何表，它使用相同的序列中重新定位值之外的下一个序列值。 (如`DBCC CHECKIDENT`的序列，但可能多个表之间的标识列等效项。)|
