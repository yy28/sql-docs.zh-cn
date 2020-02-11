---
title: WideWorldImporters OLTP 数据库目录-SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2560043ca6acc4b5df141bcbc898ac09b21f97a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68811528"
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 数据库目录
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 数据库包含销售和采购的所有事务信息和每日数据，以及车辆和冷会议室的传感器数据。

## <a name="schemas"></a>架构

WideWorldImporters 将架构用于不同目的，例如存储数据、定义用户访问数据的方式，以及提供用于数据仓库开发和集成的对象。

### <a name="data-schemas"></a>数据架构

这些架构包含数据。 所有其他架构需要多个表，并且这些表位于应用程序架构中。

|架构|说明|
|-----------------------------|---------------------|
|Application|应用程序范围内的用户、联系人和参数。 这还包含具有多个架构使用的数据的引用表|
|购买|从供应商处购买的库存项和有关供应商的详细信息。|  
|Sales|零售客户的股票销售情况以及客户和销售人员的详细信息。 |  
|Warehouse|库存物料库存和交易。|  

### <a name="secure-access-schemas"></a>安全访问架构

这些架构用于不允许直接访问数据表的外部应用程序。 它们包含外部应用程序使用的视图和存储过程。

|架构|说明|
|-----------------------------|---------------------|
|网站|来自公司网站的对数据库的所有访问都是通过此架构。|
|报表|来自 Reporting Services 报表的数据库的所有访问都通过此架构。|
|PowerBI|通过企业网关从 Power BI 仪表板对数据库的所有访问都是通过此架构来完成的。|

请注意，在示例数据库的初始版本中不使用报表和 PowerBI 架构。 但是，我们建议在此数据库之上构建的所有 Reporting Services 和 Power BI 示例使用这些架构。

### <a name="development-schemas"></a>开发架构

特殊用途的架构

|架构|说明|
|-----------------------------|---------------------|
|集成|数据仓库集成所需的对象和过程（即，将数据迁移到 WideWorldImportersDW 数据库）。|
|序列|保留应用程序中所有表使用的序列。|

## <a name="tables"></a>表

数据库中的所有表都在数据架构中。

### <a name="application-schema"></a>应用程序架构

参数和人员（用户和联系人）的详细信息，以及公用引用表（对多个其他架构通用）。

|表|说明|
|-----------------------------|---------------------|
|SystemParameters|包含系统范围的可配置参数。|
|人员|包含所有使用该应用程序的人员的用户名、联系人信息，以及由广域人员在客户组织中所涉及的人员。 这包括人员、客户、供应商和其他任何联系人。 对于已被授予使用系统或网站权限的人员，这些信息包括登录详细信息。|
|城市|系统中存储了很多地址、用户、客户组织交付地址、供应商的分拣地址等。只要存储地址，就会对此表中的城市进行引用。 每个城市还存在一个空间位置。|
|StateProvinces|城市是州或省的一部分。 此表详细说明了它们，包括描述每个州或省的边界的空间数据。|
|国家/地区|省/市/自治区是国家/地区的组成部分。 此表详细介绍了相关信息，包括描述每个国家/地区边界的空间数据。|
|DeliveryMethods|用于交付股票商品的选项（例如卡车/van、柱子、装货、柱子等）|
|PaymentMethods|用于付款的选项（例如，现金、支票、EFT 等）|
|TransactionTypes|客户、供应商或股票交易的类型（例如，发票、贷方注释等）|

### <a name="purchasing-schema"></a>采购架构

供应商和库存商品采购的详细信息。

|表|说明|
|-----------------------------|---------------------|
|Suppliers|供应商的主实体表（组织）|
|SupplierCategories|供应商的类别（例如，novelties、玩具、服装、包装等）|
|SupplierTransactions|与供应商相关的所有财务交易（发票、付款）|
|Purchaseorders.xaml|供应商采购订单的详细信息|
|PurchaseOrderLines|来自供应商采购订单的详细信息行|

 
### <a name="sales-schema"></a>销售架构

客户、销售人员和库存物品销售额的详细信息。

|表|说明|
|-----------------------------|---------------------|
|客户|客户的主实体表（组织或个人）|
|CustomerCategories|客户类别（ie 新奇商店、supermarkets 等）|
|BuyingGroups|客户组织可以是提高购买能力的组的一部分|
|CustomerTransactions|与客户相关的所有财务交易（发票、付款）|
|SpecialDeals|特价。 这可以包括固定价格、折扣或折扣百分比。|
|订单|客户订单的详细信息|
|OrderLines|来自客户订单的详细信息行|
|发票|客户发票的详细信息|
|InvoiceLines|客户发票中的详细信息行|

### <a name="warehouse-schema"></a>仓库架构

股票商品的详细信息、其控股和交易。

|表|说明|
|-----------------------------|---------------------|
|StockItems|库存项的主实体表|
|StockItemHoldings|库存项的非时态列。 这些是频繁更新的列。|
|StockGroups|用于对股票商品进行分类的组（例如，novelties、玩具、edible novelties 等）|
|StockItemStockGroups|哪些股票组（多对多）|
|颜色|库存项可以有颜色（可选）|
|PackageTypes|股票商品的打包方式（例如，盒、货箱、托盘、千克等）|
|StockItemTransactions|涵盖所有股票商品的所有变动（接收、销售、销帐）的事务|
|VehicleTemperatures|汽车冷却器的定期记录温度|
|ColdRoomTemperatures|经常性房间冷却器的定期记录温度|


## <a name="design-considerations"></a>设计注意事项

数据库设计是主观的，无法正确地设计数据库。 此数据库中的架构和表显示了有关如何设计自己的数据库的建议。

### <a name="schema-design"></a>架构设计

WideWorldImporters 使用少量的架构，因此可以很容易地理解数据库系统并演示数据库原则。  

只要有可能，数据库就会将经常查询的表共置到同一个架构，以最大程度地降低联接复杂性。

数据库架构已基于其他数据库 WWI_Preparation 中的一系列元数据表生成代码。 这为 WideWorldImporters 提供了高度的一致性、命名一致性和完整性。 有关如何生成架构的详细信息，请参阅源代码：[世界内导入/wwi-数据库](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>表设计

- 所有表都具有用于联接简易性的单列主键。
- 所有架构、表、列、索引和检查约束都具有一个 "说明" 扩展属性，该属性可用于识别对象或列的用途。 内存优化表是一项例外，因为它们当前不支持扩展属性。
- 所有外键都将自动编制索引，除非有另一个具有相同左分量的非聚集索引。
- 表中的自动编号取决于序列。 与标识列相比，这些序列更易于跨链接服务器和类似环境使用。 内存优化表使用标识列，因为它们在 SQL Server 2016 中不支持。
- 对这些表使用单个序列（TransactionID）： CustomerTransactions、SupplierTransactions 和 StockItemTransactions。 这说明一组表可以有单个序列。
- 某些列具有适当的默认值。

### <a name="security-schemas"></a>安全架构

出于安全考虑，WideWorldImporters 不允许外部应用程序直接访问数据架构。 为了隔离访问权限，WideWorldImporters 使用了不包含数据的安全访问架构，但包含视图和存储过程。 外部应用程序使用安全架构来检索允许其查看的数据。  这样，用户只能在安全访问架构中运行视图和存储过程

例如，本示例包括 Power BI 的仪表板。 外部应用程序以对 PowerBI 架构具有只读权限的用户身份从 Power BI 网关上访问这些 Power BI 的仪表板。  对于只读权限，用户只需对 PowerBI 架构具有 SELECT 和 EXECUTE 权限即可。 位于 WWI 的数据库管理员根据需要分配这些权限。

## <a name="stored-procedures"></a>存储过程

存储过程在架构中进行组织。 大多数架构用于配置或示例目的。

`Website`架构包含可由 Web 前端使用的存储过程。

`Reports`和`PowerBI`架构用于报告服务和 PowerBI 目的。 建议将此示例的任何扩展用于报告目的。

### <a name="website-schema"></a>网站架构

它们是客户端应用程序使用的过程，例如 Web 前端。

|过程|目的|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|允许人员（来自`Application.People`）访问网站。|
|ChangePassword|更改用户的密码（适用于不使用外部身份验证机制的用户）。|
|InsertCustomerOrders|允许插入一个或多个客户订单（包括订单行）。|
|InvoiceCustomerOrders|获取要开票的订单列表，并处理发票。|
|RecordColdRoomTemperatures|将传感器数据列表作为表值参数（TVP），并将数据应用于`Warehouse.ColdRoomTemperatures`临时表。|
|RecordVehicleTemperature|获取一个 JSON 数组，并使用它来`Warehouse.VehicleTemperatures`更新。|
|SearchForCustomers|按名称或名称的一部分（公司名称或人员名称）搜索客户。|
|SearchForPeople|按名称或部分名称搜索用户。|
|SearchForStockItems|按名称或部分名称或市场营销注释搜索库存项。|
|SearchForStockItemsByTags|按标记搜索库存项。|
|SearchForSuppliers|按名称或名称的一部分（公司名称或人员名称）搜索供应商。|

### <a name="integration-schema"></a>集成架构

此架构中的存储过程由 ETL 进程使用。 它们获取[ETL 包](wide-world-importers-perform-etl.md)所需的时间范围内的各种表所需的数据。

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 架构

模拟插入销售和采购的工作负荷。 主存储过程是`PopulateDataToCurrentDate`，用于将示例数据插入到当前日期。

|过程|目的|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|重新创建数据负载模拟所需的过程。 这是将数据引入当前日期所需要的。|
|Configuration_RemoveDataLoadSimulationProcedures|这会在数据模拟完成后再次删除这些过程。|
|DeactivateTemporalTablesBeforeDataLoad|删除所有临时表的临时性质，并在适用情况下应用触发器，以便可以进行更改，就像它们的应用时间早于 sys-时态表所允许的时间。|
|PopulateDataToCurrentDate|用于使数据最大为当前日期。 从初始备份还原数据库后，应在其他任何配置选项之前运行。|
|ReactivateTemporalTablesAfterDataLoad|重新建立临时表，包括检查数据一致性。 （删除关联的触发器）。|


### <a name="application-schema"></a>应用程序架构

这些过程用于配置示例。 它们用于将企业版功能应用于示例的 standard edition 版本，还用于添加审核和全文索引。

|过程|目的|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|如果成员不在角色中，则将成员添加到角色中|
|Configuration_ApplyAuditing|添加审核。 服务器审核适用于标准版数据库;为 enterprise edition 添加了其他数据库审核。|
|Configuration_ApplyColumnstoreIndexing|适当地将列`Sales.OrderLines`存储`Sales.InvoiceLines`索引应用于和和重新编制索引。|
|Configuration_ApplyFullTextIndexing|将全文索引应用`Application.People`于`Sales.Customers`、 `Purchasing.Suppliers`、和`Warehouse.StockItems`。 将`Website.SearchForPeople`、 `Website.SearchForSuppliers` `Website.SearchForCustomers`、、替换`Website.SearchForStockItemsByTags`为使用全文索引的替换过程。 `Website.SearchForStockItems`|
|Configuration_ApplyPartitioning|将表分区应用`Sales.CustomerTransactions`于`Purchasing.SupplierTransactions`和，并重新排列索引以适应。|
|Configuration_ApplyRowLevelSecurity|应用行级别安全性，按与销售区域相关的角色来筛选客户。|
|Configuration_ConfigureForEnterpriseEdition|应用列存储索引、完整文本、内存中、polybase 和分区。|
|Configuration_EnableInMemory|添加内存优化文件组（在 Azure 中不工作时），将`Warehouse.ColdRoomTemperatures`替换`Warehouse.VehicleTemperatures`为内存中等效项，并迁移数据，重新创建具有`Website.OrderIDList`内存`Website.OrderList`优化`Website.OrderLineList`等效`Website.SensorDataList`项的、和，表类型，删除并重新创建使用`Website.InvoiceCustomerOrders`这些`Website.InsertCustomerOrders`表类型`Website.RecordColdRoomTemperatures`的过程、和。|
|Configuration_RemoveAuditing|删除审核配置。|
|Configuration_RemoveRowLevelSecurity|删除行级别安全配置（对关联表的更改需要这种配置）。|
|CreateRoleIfNonExistant|如果数据库角色尚不存在，则创建该角色。|


### <a name="sequences-schema"></a>序列架构

用于在数据库中配置序列的过程。

|过程|目的|
|-----------------------------|---------------------|
|ReseedAllSequences|为所有序列调用过程 ReseedSequenceBeyondTableValue。|
|ReseedSequenceBeyondTableValue|用于将下一个序列值重定位到任何使用同一序列的表中的值之外。 （类似于标识符列的 DBCC CHECKIDENT 等效于序列但可能跨多个表）。|
