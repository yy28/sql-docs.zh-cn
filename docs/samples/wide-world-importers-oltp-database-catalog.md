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
manager: craigg
ms.openlocfilehash: e26299f221facfc6828369e1c75225f206937eb4
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579577"
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 数据库目录
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 数据库包含所有事务的信息和销售和采购，每日数据以及汽车和冷聊天室的传感器数据。

## <a name="schemas"></a>架构

WideWorldImporters 使用多种用途，例如，存储数据、 定义用户可以如何访问数据，以及为数据仓库开发和集成提供对象的架构。

### <a name="data-schemas"></a>数据架构

这些架构包含的数据。 多个表所需的所有其他架构，并且位于应用程序架构。

|架构|Description|
|-----------------------------|---------------------|
|应用程序|应用程序范围的用户、 联系人和参数。 其中还包含具有多个架构使用的数据的引用表|
|Purchasing|库存项购买从供应商和供应商有关的详细信息。|  
|Sales|库存项销售额与零售客户和客户和销售人员有关的详细信息。 |  
|Warehouse|库存商品的库存和事务。|  

### <a name="secure-access-schemas"></a>安全访问架构

不允许直接访问数据的表的外部应用程序使用这些架构。 它们包含视图和外部应用程序使用的存储的过程。

|架构|Description|
|-----------------------------|---------------------|
|网站|从公司网站到数据库的所有访问都都通过此架构。|
|报表|从 Reporting Services 报表到数据库的所有访问都都通过此架构。|
|PowerBI|到数据库中的 Power BI 仪表板通过企业网关的所有访问都都通过此架构。|

请注意，报表和 power Bi 示例数据库的初始版本中不使用架构。 但是，建议基于此数据库的所有 Reporting Services 和 Power BI 示例使用这些架构。

### <a name="development-schemas"></a>开发架构

特殊用途的架构

|架构|Description|
|-----------------------------|---------------------|
|集成|对象和数据仓库集成所需的过程 （即将数据迁移到 WideWorldImportersDW 数据库）。|
|序列|存储由应用程序中的所有表的序列。|

## <a name="tables"></a>表

在数据库中的所有表都位于数据架构中。

### <a name="application-schema"></a>应用程序架构

参数和用户 （用户和联系人），以及公共 （常见到多个其他架构） 的引用表的详细信息。

|表|Description|
|-----------------------------|---------------------|
|SystemParameters|包含系统范围内的可配置参数。|
|人员|包含用户名的所有用户使用该应用程序和 Wide World Importers 处理的客户组织的人员的联系信息。 这包括员工、 客户、 供应商和其他联系人。 对于已被授予权限以使用系统或网站的人员，这些信息包括登录名的详细信息。|
|城市|有许多存储在系统中，对于人员，客户组织传递地址，在供应商等拾取地址的地址。存储一个地址，只要没有对此表中的城市的引用。 此外，还有每个城市的空间位置。|
|StateProvinces|城市是州或省的一部分。 此表提供的工具，包括描述边界的空间数据的详细信息，每个州或省。|
|国家/地区|州或省是国家/地区的一部分。 此表提供工具，包括描述每个国家/地区的边界的空间数据的详细的信息。|
|DeliveryMethods|交付股票项 （例如，卡车/van、 post、 提取、 媒体等） 的选择|
|PaymentMethods|使付款选项 (例如，现金、 检查，EFT，等等。)|
|TransactionTypes|类型的客户、 供应商或股票交易记录 （例如，发票、 贷记等）|

### <a name="purchasing-schema"></a>购买架构

供应商提供的和的库存项购买的详细信息。

|表|Description|
|-----------------------------|---------------------|
|Suppliers|供应商 （组织） 的主实体表|
|SupplierCategories|供应商 （例如，novelties、 玩具、 clothing，打包，等等） 的类别|
|SupplierTransactions|所有的财务交易记录供应商相关 （发票付款）。|
|PurchaseOrders|供应商的采购订单的详细信息|
|PurchaseOrderLines|从供应商的详细信息行采购订单|

 
### <a name="sales-schema"></a>销售架构

和库存物料销售额的客户，销售人员的详细信息。

|表|Description|
|-----------------------------|---------------------|
|Customers|客户 （组织或个人） 的主实体表|
|CustomerCategories|客户 （即新奇存储、 超市等） 的类别|
|BuyingGroups|客户组织可以是进行购买更强大的功能的组的一部分|
|CustomerTransactions|所有的财务交易记录客户相关 （发票付款）。|
|SpecialDeals|特价优惠。 这可以包括固定的价格，以美元为单位或折扣百分比折扣。|
|Orders|客户订单的详细信息|
|订单行|从客户订单的详细信息行|
|发票|客户发票的详细信息|
|InvoiceLines|从客户发票的详细信息行|

### <a name="warehouse-schema"></a>仓库架构

常用项、 其 holdings 和事务的详细信息。

|表|Description|
|-----------------------------|---------------------|
|StockItems|主实体表以获取股票项目|
|StockItemHoldings|常用项的非临时列。 这些是经常更新的列。|
|StockGroups|用于将分类股票项 （例如，novelties、 玩具、 edible novelties 等） 的组|
|StockItemStockGroups|哪些股票项目是 stock 分组 （多对多）|
|颜色|常用项 （可选） 可以具有颜色|
|PackageTypes|可以打包库存物料的方式 （例如，框、 纸箱、 货盘、 kg，等等。|
|StockItemTransactions|涵盖所有常用的项 （回执、 销售、 勾销） 的所有动作的事务|
|VehicleTemperatures|车辆冷却器的定期记录的温度|
|ColdRoomTemperatures|定期记录的冷聊天室冷却器的温度|


## <a name="design-considerations"></a>设计注意事项

数据库设计是一个主观问题并没有正确或错误方法来设计数据库。 架构和此数据库中的表显示为如何设计您自己的数据库提出的建议。

### <a name="schema-design"></a>架构设计

WideWorldImporters 使用少量的架构，因此很容易地了解数据库系统和演示数据库原则。  

如有可能，该数据库并置到同一架构，以最大程度减少联接复杂性经常查询的表。

数据库架构已被代码生成基于一系列的另一个数据库 WWI_Preparation 中的元数据表。 这样，WideWorldImporters 极高的设计的一致性、 命名一致性和完整性。 有关如何生成架构的详细信息，请参阅源代码：[范围内的世界-导入程序/wwi-数据库的脚本](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>表设计

- 所有表都具有单个列主键联接为了简单起见。
- 所有架构、 表、 列、 索引和 check 约束都有扩展属性，可用于标识对象或列的用途说明。 内存优化表是一种例外，因为它们当前不支持扩展的属性。
- 如果没有具有相同的左侧组件的另一个非聚集索引，所有外键将自动编制索引。
- 自动编号在表中基于序列。 这些序列是更轻松地使用链接的服务器和类似环境比标识列。 内存优化表使用标识列，因为它们不支持在 SQL Server 2016 中。
- 单个序列 (TransactionID) 用于这些表：CustomerTransactions、 SupplierTransactions 和 StockItemTransactions。 此示例演示如何使一组表具有一个序列。
- 某些列具有适当的默认值。

### <a name="security-schemas"></a>安全架构

为了安全，WideWorldImporters 不允许外部应用程序直接访问数据的架构。 若要隔离访问，WideWorldImporters 将使用不包含数据，但包含视图和存储的过程的安全访问权限架构。 外部应用程序使用的安全架构检索允许他们查看的数据。  这样一来，用户只能运行视图和存储的过程中的安全访问架构

例如，此示例包括 Power BI 仪表板。 外部应用程序访问这些 Power BI 仪表板从 Power BI 网关作为 power Bi 中的架构具有只读权限的用户。  对于只读权限，用户只需要具有 power Bi 架构的 SELECT 和 EXECUTE 权限。 WWI 数据库管理员将根据需要分配这些权限。

## <a name="stored-procedures"></a>存储过程

在架构中进行组织的存储的过程。 大部分架构用于配置或示例用途。

`Website`架构包含可由 Web 前端的存储的过程。

`Reports`和`PowerBI`架构用于 reporting services 和 power Bi 目的。 示例的任何扩展且建议用于报告目的使用这些架构。

### <a name="website-schema"></a>网站架构

这些是由客户端应用程序，如 Web 前端的过程。

|过程|目标|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|让用户 (从`Application.People`) 以有权访问该网站。|
|ChangePassword|更改用户的密码 （适用于不使用外部身份验证机制的用户）。|
|InsertCustomerOrders|允许插入 （包括订单行） 的一个或多个客户订单。|
|InvoiceCustomerOrders|采用一系列订单开发票并处理发票。|
|RecordColdRoomTemperatures|使用传感器数据列表，作为表值参数 (TVP)，并应用到数据`Warehouse.ColdRoomTemperatures`临时表。|
|RecordVehicleTemperature|将 JSON 数组并使用它来更新`Warehouse.VehicleTemperatures`。|
|SearchForCustomers|按名称或部分名称 （公司名称或人员姓名） 客户的搜索。|
|SearchForPeople|搜索人员按名称或名称的一部分。|
|SearchForStockItems|按名称或名称或市场营销注释的一部分的股票项搜索。|
|SearchForStockItemsByTags|按标记的股票项搜索。|
|SearchForSuppliers|按名称或名称 （公司名称或人员姓名） 的一部分的供应商的搜索。|

### <a name="integration-schema"></a>集成架构

ETL 过程使用此架构中的存储的过程。 他们获得所需的时间范围的不同表中所需的数据[ETL 包](wide-world-importers-perform-etl.md)。

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 架构

模拟插入销售和采购的工作负荷。 主存储的过程是`PopulateDataToCurrentDate`，用于插入截至当前日期的示例数据。

|过程|目标|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|重新创建过程的数据所需负载模拟。 这需要将数据添加至当前日期。|
|Configuration_RemoveDataLoadSimulationProcedures|数据模拟完成后，这再次删除过程。|
|DeactivateTemporalTablesBeforeDataLoad|删除所有临时表的临时特性，并在适用的情况下，应用触发器，以便可以进行更改，就好像它们已在以前的日期不是 sys 时态表允许正在应用。|
|PopulateDataToCurrentDate|用于引入截至当前日期的数据。 之前，应运行从一个初始备份还原数据库之后的任何其他配置选项。|
|ReactivateTemporalTablesAfterDataLoad|重新建立临时表，其中包括的数据一致性检查。 （将删除关联的触发器）。|


### <a name="application-schema"></a>应用程序架构

使用这些过程来配置示例。 它们用于企业版功能适用于 standard edition 版本的示例，还可添加审核和全文索引。

|过程|目标|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|如果该成员不是角色中向角色添加成员|
|Configuration_ApplyAuditing|Adds 审核。 服务器审核适用于标准版本的数据库。对于 enterprise edition 添加附加的数据库审核。|
|Configuration_ApplyColumnstoreIndexing|将应用到索引的列存储`Sales.OrderLines`和`Sales.InvoiceLines`并相应地重新编制索引。|
|Configuration_ApplyFullTextIndexing|将应用到全文索引`Application.People`， `Sales.Customers`， `Purchasing.Suppliers`，和`Warehouse.StockItems`。 将替换`Website.SearchForPeople`， `Website.SearchForSuppliers`， `Website.SearchForCustomers`， `Website.SearchForStockItems`，`Website.SearchForStockItemsByTags`与使用全文索引编制的更换过程。|
|Configuration_ApplyPartitioning|将应用到的表分区`Sales.CustomerTransactions`和`Purchasing.SupplierTransactions`，和重新排列的索引以满足。|
|Configuration_ApplyRowLevelSecurity|应用于筛选器的客户的行级别安全性，方法是 sales territory 相关角色。|
|Configuration_ConfigureForEnterpriseEdition|将应用列存储索引、 全文、 内存中，polybase 和分区。|
|Configuration_EnableInMemory|（如果不在 Azure 中运行） 中添加内存优化文件组，将替换`Warehouse.ColdRoomTemperatures`，`Warehouse.VehicleTemperatures`与内存中的等效项，并会将数据迁移，将重新创建`Website.OrderIDList`， `Website.OrderList`， `Website.OrderLineList`，`Website.SensorDataList`表使用的类型内存优化的等效项、 删除和重新创建过程`Website.InvoiceCustomerOrders`， `Website.InsertCustomerOrders`，和`Website.RecordColdRoomTemperatures`，它使用这些表类型。|
|Configuration_RemoveAuditing|删除的审核配置。|
|Configuration_RemoveRowLevelSecurity|删除行级别安全性 （这所需的配置对关联的表的更改）。|
|CreateRoleIfNonExistant|如果它尚不存在，请创建一个数据库角色。|


### <a name="sequences-schema"></a>序列架构

若要配置数据库中的序列的过程。

|过程|目标|
|-----------------------------|---------------------|
|ReseedAllSequences|为所有序列调用过程 ReseedSequenceBeyondTableValue。|
|ReseedSequenceBeyondTableValue|用于在任何表，它使用相同的序列中重新定位值之外的下一个序列值。 （如 DBCC CHECKIDENT 为标识列等效的序列，但可能多个表之间)。|
