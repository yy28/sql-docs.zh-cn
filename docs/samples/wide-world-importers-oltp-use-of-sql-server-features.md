---
title: 使用 SQL Server 特性和功能 |Microsoft 文档
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
caps.latest.revision: 2
author: MashaMSFT
ms.author: mathoma
manager: craigg
robots: noindex,nofollow
ms.openlocfilehash: 01d53c67e54ab9a0a4c2e5dd8ab4e5441fd8db4a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="use-of-sql-server-features-and-capabilities"></a>使用 SQL Server 功能和功能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 使用 SQL Server 特性和 OLTP 数据库中的功能。

WideWorldImporters 旨在展示许多 SQL Server，包括 SQL Server 2016 中引入的最新功能的主要功能。 下面是 SQL Server 功能和功能，以及如何在 WideWorldImporters 中使用的说明的列表。

|SQL Server 功能或功能|在 WideWorldImporters 中的使用|
|-----------------------------|---------------------|
|临时表|有多个临时表，包括所有查找样式引用表和主要的实体，例如 StockItems、 客户和供应商。 允许使用临时表来方便地跟踪这些实体的历史记录。|
|For JSON 的 AJAX 调用|应用程序经常使用 AJAX 调用来查询这些表中： 人员、 客户、 供应商和 StockItems。 在调用返回 JSON 有效负载 （即返回的数据的格式为 JSON 数据时）。 请参阅，例如，存储的过程`Website.SearchForCustomers`。|
|JSON 属性/值包|多个表具有保存 JSON 数据来扩展表中的关系数据的列。 例如，`Application.SystemParameters`有一列用于应用程序设置和`Application.People`已记录的用户首选项的列。 这些表使用`nvarchar(max)`列来记录的 JSON 数据，以及使用内置函数的 CHECK 约束`ISJSON`以确保列的值为有效的 JSON。|
|行级别安全性 (RLS)|行级别安全性 (RLS) 用于限制对 Customers 表，基于角色的成员资格访问。 每个销售区域拥有的角色和用户。 若要查看此操作中，使用相应中的脚本示例-script.zip，是一部分的[版本的示例](http://go.microsoft.com/fwlink/?LinkID=800630)。|
|实时运行分析|（完整版本的数据库）核心事务表`Sales.InvoiceLines`和`Sales.OrderLines`都具有可用于高效地执行分析查询支持带有上操作工作负载的影响最小的事务数据库中的非聚集列存储索引。 运行在同一数据库中的事务和分析也称为[混合事务/分析处理 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))。 若要查看此操作中，使用相应中的脚本示例-script.zip，是一部分的[版本的示例](http://go.microsoft.com/fwlink/?LinkID=800630)。|
|PolyBase|若要查看此操作中的 PolyBase 使用外部表使用托管在 Azure 博客存储较公用数据集使用相应的脚本示例-script.zip，是一部分中的[版本的示例](http://go.microsoft.com/fwlink/?LinkID=800630)。|
|内存中 OLTP|（完整版本的数据库）表类型是所有内存优化，以便从内存优化的表值参数 (Tvp 所有) 受益。<br/><br/>两个监视表，`Warehouse.VehicleTemperatures`和`Warehouse.ColdRoomTemperatures`，是内存优化。 这允许 ColdRoomTemperatures 表以填充在更高的速度比传统的基于磁盘的表。 VehicleTemperatures 表保持 JSON 负载，并本身适于针对 IoT 进行扩展。 VehicleTemperatures 表进一步为本身适于涉及 EventHubs、 流分析和 Power BI 的方案。<br/><br/>存储的过程`Website.RecordColdRoomTemperatures`本机编译后可进一步提高性能的录制冷聊天室温度。<br/><br/>若要查看在操作中内存中 OLTP 的示例，请参阅中工作负荷-drivers.zip，是一部分的车辆位置工作负荷驱动程序的[版本的示例](http://go.microsoft.com/fwlink/?LinkID=800630)。|
|聚集列存储索引|（完整版本的数据库）表`Warehouse.StockItemTransactions`使用聚集列存储索引。 此表中的行数应变大，且聚集列存储索引可显著减小的磁盘上大小的表，和可以提高查询性能。 在此表上的进行修改是插入只-不没有在此表中联机工作负荷的任何更新/删除，聚集列存储索引执行适用于插入工作负荷。|
|动态数据屏蔽|在数据库架构中，数据屏蔽已应用到持有供应商，表中的 bank 详细信息`Purchasing.Suppliers`。 非管理员人员不会访问此信息。|
|始终加密|Always encrypted 演示纳入可下载 samples.zip，即一部分的[版本的示例](http://go.microsoft.com/fwlink/?LinkID=800630)... 演示创建加密密钥，对敏感数据，以及将数据插入到表的小的示例应用使用加密的表。|
|延伸数据库|`Warehouse.ColdRoomTemperatures`表已实现为临时表，并且它是内存优化的示例数据库的完整版本。 存档表是基于磁盘的并可以扩展到 Azure。|
|全文索引|全文本索引可提高搜索人员、 客户和 StockItems。 仅当你具有 SQL Server 实例上安装的全文索引，索引将应用于查询。 非持久化计算的列用于创建为全文索引 StockItems 表中的数据。<br/><br/>`CONCAT` 用于连接的字段创建 SearchData 是全文索引。<br/>若要启用的全文索引，在此示例中使用数据库中执行以下语句：<br/><br/>    `EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>该过程创建默认的全文目录如果一个尚不存在，则替换全文本版本的这些视图搜索视图）。<br/><br/>请注意，在 SQL Server 中使用的全文索引需要选择在安装过程中的全文索引选项。 Azure SQL 数据库不需要和特定配置，以启用的全文索引。|
|索引的持久化计算的列|索引在 SupplierTransactions 和 CustomerTransactions 中使用的持久化计算的列。|
|检查约束|相对较为复杂的 check 约束处于`Sales.SpecialDeals`。 这样可以确保一个且只有一个 DiscountAmount，DiscountPercentage，并且单价进行配置。|
|唯一约束|多对多个构造 （和唯一约束） 是为 Warehouse.StockItemStockGroups 的设置。|
|表分区|（完整版本的数据库）表`Sales.CustomerTransactions`和`Purchasing.SupplierTransactions`同时分区按年使用分区函数`PF_TransactionDate`和分区方案`PS_TransactionDate`。 分区用于改进大型表的可管理性。|
|列表处理|示例表类型`Website.OrderIDList`提供。 它由示例过程`Website.InvoiceCustomerOrders`。 过程使用公用表表达式 (Cte)、 TRY/CATCH、 JSON_MODIFY、 XACT_ABORT、 NOCOUNT、 THROW 和 XACT_STATE 演示处理订单，而不是只需单个订单，尽量减小在应用程序中对数据库引擎的往返过程的列表的能力。|
|GZip 压缩|`Warehouse.VehicleTemperature`的表保存完整的传感器数据，但此数据是旧的多个使用几个月，当它被压缩，以节省空间使用 COMPRESS 函数，使用 GZip 压缩。<br/><br/>该视图`Website.VehicleTemperatures`检索以前压缩的数据时使用 DECOMPRESS 函数。|
|查询存储|Query Store 在数据库上启用。 运行几个查询之后, 在 Management Studio 中打开数据库，打开节点 Query Store，这是该数据库下，并打开报表顶部资源使用的查询以查看查询执行和查询的计划，只需运行。|
|STRING_SPLIT|列`DeliveryInstructions`表中`Sales.Invoices`具有可以用于演示 STRING_SPLIT 的以逗号分隔的值。|
|审核|可以在数据库中运行以下语句，为此示例数据库启用 SQL Server Audit:<br/><br/>    `EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>通过启用了 Azure SQL 数据库审核[Azure 门户](https://portal.azure.com/)。<br/><br/>角色和权限涉及登录名的安全操作，登录审核 （包括标准版的系统） 的启用其中的所有系统。 审核定向到应用程序日志中，因为这是适用于所有系统，不需要其他权限。 警告由于是为了提高安全性，它应可重定向到安全日志或一个安全的文件夹中的文件。 提供的链接来描述所需的其他配置。<br/><br/>对于评估/开发人员/企业版系统，审核对所有财务事务数据的访问。|
