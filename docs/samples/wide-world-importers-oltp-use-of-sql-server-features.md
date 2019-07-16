---
title: 使用 SQL Server 特性和功能 |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 01/21/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a2dfe7b9efa78d03a2233eedaa040e47d6f2b25c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067658"
---
# <a name="use-of-sql-server-features-and-capabilities"></a>使用 SQL Server 功能和功能

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

WideWorldImporters 使用的 SQL Server 功能和 OLTP 数据库中的功能。

WideWorldImporters 旨在展示的许多关键功能的 SQL Server，包括 SQL Server 2016 中引入的最新功能。 下表列出了特性和功能的 SQL Server。 每个行还提供了如何在 WideWorldImporters 中使用功能的说明。  
&nbsp;

|SQL Server 功能或功能|在 WideWorldImporters 中的使用|
|:-------------------------------|:------------------------|
|临时表|有多个临时表，其中包括所有查找样式引用表和主实体，例如 StockItems、 客户和供应商。 使用临时表，以方便地跟踪这些实体的历史记录。|
|为 JSON 的 AJAX 调用|应用程序经常使用的 AJAX 调用来查询这些表：人员、 客户、 供应商和 StockItems。 调用以 JSON 格式返回数据。 有关示例，请参阅存储的过程`Website.SearchForCustomers`。|
|JSON 属性/值包|多个表包含保存要扩展表中的关系数据的 JSON 数据的列。 例如，`Application.SystemParameters`有一列用于应用程序设置和`Application.People`有一列对记录用户首选项。 这些表使用`nvarchar(max)`记录的 JSON 数据，以及使用内置函数的 CHECK 约束的列`ISJSON`以确保列的值为有效的 JSON。|
|行级别安全性 (RLS)|行级别安全性 (RLS) 用于限制对 Customers 表中，基于角色的成员身份的访问。 每个销售区域均包含一个角色和用户。 若要查看的 RLS 访问限制在操作中，请使用相应的脚本示例-script.zip 中包含的[版本的示例](https://go.microsoft.com/fwlink/?LinkID=800630)。|
|实时运行分析|（完整版本的数据库）核心事务表`Sales.InvoiceLines`和`Sales.OrderLines`都具有可用于支持在对操作工作负荷的影响最小的事务数据库中高效执行分析查询的非聚集列存储索引。 在同一数据库中运行的事务和分析也称为[混合事务/分析处理 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))。 若要了解此操作，请使用相应的脚本示例-script.zip，这是部分中的[版本的示例](https://go.microsoft.com/fwlink/?LinkID=800630)。|
|PolyBase|若要查看在操作中，此 PolyBase 使用外部表使用托管在 Azure 博客存储中的公共数据集使用相应的脚本示例-script.zip，这是部分中的[版本的示例](https://go.microsoft.com/fwlink/?LinkID=800630)。|
|内存中 OLTP|（完整版本的数据库）表类型是所有内存优化，以便从内存优化的表值参数 (Tvp 所有) 受益。<br/><br/>两个监视表`Warehouse.VehicleTemperatures`和`Warehouse.ColdRoomTemperatures`，是内存优化。 内存优化允许在更高的速度比传统的基于磁盘的表填充 ColdRoomTemperatures 表。 VehicleTemperatures 表包含 JSON 有效负载，并将租借自身以便向 IoT 方案的扩展。 进一步 VehicleTemperatures 表适合涉及 EventHubs、 Stream Analytics 和 Power BI 的方案。<br/><br/>存储的过程`Website.RecordColdRoomTemperatures`本机编译来进一步提高性能的录制冷的房间温度。<br/><br/>若要查看操作中的内存中 OLTP 示例，请参阅工作负荷-drivers.zip，这是部分中的车辆位置工作负载驱动程序的[版本的示例](https://go.microsoft.com/fwlink/?LinkID=800630)。|
|聚集列存储索引|（完整版本的数据库）表`Warehouse.StockItemTransactions`使用聚集列存储索引。 预期的此表中的行数会变得很大，并且聚集列存储索引显著减少了磁盘上大小的表，并可以提高查询性能。 对此表的修改是只插入-不没有对此表中联机工作负荷的任何更新/删除，聚集列存储索引执行适合插入工作负荷。|
|动态数据屏蔽|在数据库架构中，数据掩码已应用到表中持有供应商的银行详细信息`Purchasing.Suppliers`。 非管理人员不会访问此信息。|
|始终加密|Always encrypted 演示包含在可下载 samples.zip，它是一部分的[版本的示例](https://go.microsoft.com/fwlink/?LinkID=800630)。 演示创建加密密钥，对敏感数据，以及将数据插入到表的小型示例应用程序使用加密的表。|
|Stretch Database|`Warehouse.ColdRoomTemperatures`表已实现为临时表，并且它是内存优化的示例数据库的完整版本中。 存档表是基于磁盘的并被拉伸到 Azure。|
|全文索引|全文索引可提高搜索的人、 客户和 StockItems。 仅在具有 SQL Server 实例上安装全文索引，索引将应用于查询。 非持久化计算的列用于创建为全文索引 StockItems 表中的数据。<br/><br/>`CONCAT` 用于连接字段创建 SearchData 是全文索引。<br/>若要启用示例中的全文索引的使用，请在数据库中执行以下语句：<br/><br/>`EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>该过程创建一个默认全文目录如果其中一个尚不存在，则将使用这些视图的全文索引版本替换搜索视图）。<br/><br/>请注意，使用 SQL Server 中的全文索引要求选择在安装过程中的全文索引选项。 Azure SQL 数据库不需要和特定配置，以启用全文索引。|
|索引的持久化计算的列|编制索引 SupplierTransactions 和 CustomerTransactions 中使用的持久化计算的列。|
|检查约束|在相对较复杂的 check 约束是`Sales.SpecialDeals`。 这可确保一个并且只有一个 DiscountAmount，DiscountPercentage，并且单价进行配置。|
|唯一约束|多对多个构造 （和唯一约束） 设置了`Warehouse.StockItemStockGroups`。|
|表分区|（完整版本的数据库）表`Sales.CustomerTransactions`并`Purchasing.SupplierTransactions`都分区使用分区函数的年份`PF_TransactionDate`和分区方案`PS_TransactionDate`。 使用分区来提高大型表的可管理性。|
|列表处理|示例表类型`Website.OrderIDList`提供。 示例过程使用`Website.InvoiceCustomerOrders`。 该过程使用公用表表达式 (Cte)、 TRY/CATCH，JSON_MODIFY、 XACT_ABORT、 NOCOUNT、 THROW 和 XACT_STATE 演示处理的订单，而不只是单个订单，若要最大程度减少往返行程，应用程序中对列表的功能数据库引擎。|
|GZip 压缩|在`Warehouse.VehicleTemperature`视图，其表保留完整的传感器数据。 但旧的多个几个月此数据时，它经过压缩以节省空间。 COMPRESS 函数使用 GZip 压缩。<br/><br/>该视图`Website.VehicleTemperatures`检索以前压缩的数据时使用 DECOMPRESS 函数。|
|查询存储|对数据库启用查询存储。 运行后几个查询，执行以下步骤：<br/><br/>1.在 Management Studio 中打开数据库。<br/>2.打开查询存储，这是该数据库下的节点。<br/>3.打开报表*热门资源使用查询*。 请参阅查询执行，并查看个查询只需运行的计划。|
|STRING_SPLIT|该列`DeliveryInstructions`表中`Sales.Invoices`可用于演示 STRING_SPLIT 的以逗号分隔的值。|
|审核|可以在数据库中运行以下语句，为此示例数据库启用 SQL Server 审核：<br/><br/>`EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>通过启用了 Azure SQL 数据库审核[Azure 门户](https://portal.azure.com/)。<br/><br/>角色和权限涉及登录名的安全操作，登录审核 （包括标准版系统） 的启用了所有系统。 审核被定向到应用程序日志，因为这是适用于所有系统，不需要其他权限。 警告是考虑到为了提高安全性，它应被重定向到安全日志或安全文件夹中的文件。 提供的链接来描述所需的其他配置。<br/><br/>对于评估/开发人员/企业版的系统，对所有财务事务数据的访问进行审核。|
| &nbsp; | &nbsp; |
