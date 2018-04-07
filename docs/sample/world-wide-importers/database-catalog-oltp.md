---
title: WideWorldImporters 数据库目录 |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e47c0022-ce87-4ba5-a24b-df55efe66431
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 0d458bc15530aa87bfa922787558fff3f07645f7
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2018
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 数据库目录
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 数据库包含所有事务信息和销售和采购，每日数据以及汽车和冷聊天室的传感器数据。

## <a name="schemas"></a>架构

WideWorldImporters 用于不同用途，例如存储数据、 定义用户可以如何访问数据，并为数据仓库开发和集成提供对象的架构。

### <a name="data-schemas"></a>数据架构

这些架构包含的数据。 多个表所需的所有其他架构，并位于应用程序架构。

|架构|Description|
|-----------------------------|---------------------|
|应用程序|应用程序范围的用户、 联系人和参数。 这还包含由多个架构的数据与引用表|
|Purchasing|常用项购买从供应商和供应商有关的详细信息。|  
|Sales|股票项销售零售客户和客户和销售人员有关的详细信息。 |  
|Warehouse|常用项清单和事务。|  

### <a name="secure-access-schemas"></a>安全访问架构

不允许直接访问数据的表的外部应用程序使用这些架构。 它们包含视图和外部应用程序使用的存储的过程。

|架构|Description|
|-----------------------------|---------------------|
|网站|从公司网站到数据库的所有访问都都通过此架构。|
|报表|到数据库从 Reporting Services 报表的所有访问都都通过此架构。|
|PowerBI|从 Power BI 仪表板，通过企业网关到数据库的所有访问都都通过此架构。|

请注意，报表和 PowerBI 示例数据库的初始版本中不使用架构。 但是，基于此数据库的所有 Reporting Services 和 Power BI 示例还鼓励使用这些架构。

### <a name="development-schemas"></a>开发架构

特殊用途架构

|架构|Description|
|-----------------------------|---------------------|
|集成|对象和数据仓库集成所需的过程 （即将数据迁移到 WideWorldImportersDW 数据库）。|
|序列|包含由应用程序中的所有表的序列。|

## <a name="tables"></a>表

在数据库中的所有表都位于数据架构中。

### <a name="application-schema"></a>应用程序架构

参数和人员 （用户和联系人），以及常见 （普遍适用于多个其他架构） 的引用表的详细信息。

|表|Description|
|-----------------------------|---------------------|
|SystemParameters|包含整个系统可配置参数。|
|人员|包含用户名称，所有用户使用应用程序，和 Wide World Importers 处理在客户组织的人员的联系信息。 这包括员工、 客户、 供应商和任何其他联系人。 对于用户已被授予权限以使用系统或网站，这些信息包括登录详细信息。|
|城市|有许多地址存储在系统中，对于人来说，客户组织交付地址，选取地址在供应商，等等。只要地址还存储，就没有对此表中的城市的引用。 此外，还有每个城市的空间位置。|
|StateProvinces|城市是州或省的一部分。 此表具有其中包括描述边界的空间数据的详细信息，每个州或省份。|
|国家/地区|州或省是国家/地区的一部分。 此表具有其中包括描述每个国家/地区的边界的空间数据的详细信息。|
|DeliveryMethods|选择用于传送常用项 （例如，truck/van、 post、 拾取、 媒体等。）|
|PaymentMethods|为使付款的选择 (例如，现金、 检查，EFT，等等。)|
|TransactionTypes|类型的客户、 供应商或股票交易记录 （例如，发票、 信用额度注意等）|

### <a name="purchasing-schema"></a>购买架构

供应商提供和的常用项购买的详细信息。

|表|Description|
|-----------------------------|---------------------|
|Suppliers|供应商 （组织） 的主实体表|
|SupplierCategories|供应商 （例如，novelties、 toys，服装，打包，等等） 的类别|
|SupplierTransactions|所有的财务交易记录供应商相关 （发票付款）。|
|PurchaseOrders|供应商的采购订单的详细信息|
|PurchaseOrderLines|从供应商的详细信息行采购订单|

 
### <a name="sales-schema"></a>销售架构

详细信息的客户，销售人员，和的库存物料销售额。

|表|Description|
|-----------------------------|---------------------|
|客户|客户 （组织或个人） 的主实体表|
|CustomerCategories|客户 （即新奇存储、 超市等） 的类别|
|BuyingGroups|客户组织可以是施加更高的购买能力的组的一部分|
|CustomerTransactions|所有的财务交易记录客户相关 （发票付款）。|
|SpecialDeals|特殊定价。 这可以包括固定的价格，折扣资金或折扣百分比。|
|Orders|客户订单的详细信息|
|订单行|从客户订单的详细信息行|
|发票|客户发票详细信息|
|InvoiceLines|从客户发票详细信息行|

### <a name="warehouse-schema"></a>仓库架构

常用的项、 其控股和事务的详细信息。

|表|Description|
|-----------------------------|---------------------|
|StockItems|常用的项的主实体表|
|StockItemHoldings|常用的项的非临时列。 这些是经常更新的列。|
|StockGroups|用于分类 （例如，novelties、 toys、 edible novelties 等） 的常用项组|
|StockItemStockGroups|哪些股票项目是 stock 分组 （多对多）|
|颜色|常用的项 （可选） 可以具有颜色|
|PackageTypes|可以打包库存物料的方式 （例如，框、 carton、 调色板、 公斤，等等。|
|StockItemTransactions|涵盖的所有常用的项 （回执、 销售、 注销） 的所有动作数的事务|
|VehicleTemperatures|车辆冷却设备的定期记录的温度|
|ColdRoomTemperatures|定期记录温度冷聊天室冷却设备|


## <a name="design-considerations"></a>设计注意事项

数据库设计是主观和没有右或错误方法来设计数据库。 架构和此数据库中的表显示了如何可以设计自己的数据库为提出的建议。

### <a name="schema-design"></a>架构设计

WideWorldImporters 使用少量的架构，因此，很容易地了解数据库系统，并演示数据库原则。  

只要有可能，数据库将配置到相同的架构，以最小化联接复杂性常用查询的表。

数据库架构已生成的代码基于一系列的另一个数据库 WWI_Preparation 中的元数据表。 这样，WideWorldImporters 非常高的设计的一致性，命名一致性和完整性。 有关如何生成架构的详细信息，请参阅源代码：[范围的实际-导入程序/wwi-数据库的脚本](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>表设计

- 所有表都具有单个列主键联接为了简单起见。
- 所有架构、 表、 列、 索引和检查约束都具有扩展属性，可以用于标识对象或列的用途的说明。 内存优化表是一种例外，因为它们当前不支持扩展的属性。
- 如果没有具有相同的左侧组件的另一个非聚集索引，所有外键会自动编制索引。
- 表中自动编号取决于序列。 更轻松地使用跨链接的服务器和与标识列的类似环境中这些序列。 内存优化表使用标识列，因为它们不支持在 SQL Server 2016 中。
- 一个序列 (TransactionID) 用于这些表： CustomerTransactions、 SupplierTransactions 和 StockItemTransactions。 此示例演示如何一组表可以有一个序列。
- 某些列具有适当的默认值。

### <a name="security-schemas"></a>安全架构

为安全起见，WideWorldImporters 不允许外部应用程序直接访问数据架构。 若要隔离访问，WideWorldImporters，请使用安全访问架构不具有相关数据，但包含视图和存储的过程。 外部应用程序使用的安全架构检索允许他们查看的数据。  这样一来，用户只能运行的视图和存储的过程中的安全访问架构

例如，此示例包括 Power BI 仪表板。 外部应用程序作为 PowerBI 架构具有只读权限的用户从 Power BI 网关访问这些 Power BI 仪表板。  对于只读权限，用户只需选择和执行权限 PowerBI 架构。 数据库管理员在 WWI 将根据需要分配这些权限。

## <a name="stored-procedures"></a>存储过程

存储的过程都组织在架构中。 大部分架构用于配置或示例目的。

`Website`架构包含可由 Web 前端的存储的过程。

`Reports`和`PowerBI`架构用于 reporting services 和 PowerBI 目的。 任何扩展示例还鼓励使用这些架构用于报告的数据。

### <a name="website-schema"></a>网站架构

这些是客户端应用程序，如 Web 前端使用的过程。

|过程|用途|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|允许个人 (从`Application.People`) 有权访问该网站。|
|ChangePassword|更改用户的密码 （适用于未使用外部身份验证机制的用户）。|
|InsertCustomerOrders|允许插入 （包括订单行） 的一个或多个客户订单。|
|InvoiceCustomerOrders|采用要开票订单的列表，并处理发票。|
|RecordColdRoomTemperatures|采用传感器数据列表中，作为表值参数 (TVP)，并应用到数据`Warehouse.ColdRoomTemperatures`临时表。|
|RecordVehicleTemperature|接受 JSON 数组，并使用它来更新`Warehouse.VehicleTemperatures`。|
|SearchForCustomers|按名称或名称 （公司名称或人员姓名） 的一部分的客户搜索。|
|SearchForPeople|按名称或名称的一部分的人员的搜索。|
|SearchForStockItems|按名称或名称或市场营销注释的一部分的常用项的搜索。|
|SearchForStockItemsByTags|通过标记的常用项的搜索。|
|SearchForSuppliers|按名称或名称 （公司名称或人员姓名） 的一部分的供应商的搜索。|

### <a name="integration-schema"></a>集成架构

此架构中的存储的过程使用 ETL 过程。 获得所需的时间范围的各种表中所需的数据[ETL 包](etl-workflow.md)。

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 架构

模拟插入销售和采购工作负荷。 主存储的过程是`PopulateDataToCurrentDate`，用于插入截至当前日期的示例数据。

|过程|用途|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|重新创建过程的数据所需负载模拟。 这需要将截至当前日期的数据。|
|Configuration_RemoveDataLoadSimulationProcedures|这将删除过程再次完成数据模拟后。|
|DeactiveTemporalTablesBeforeDataLoad|删除所有临时表的临时性质和 （如果适用），适用触发器，以便可以进行更改，就像在更早日期不是 sys 临时表允许应用它们。|
|PopulateDataToCurrentDate|用来截至当前日期的数据。 应在从初始备份还原数据库之后的任何其他配置选项之前运行。|
|ReactivateTemporalTablesAfterDataLoad|重新建立临时表，包括数据一致性检查。 （将删除关联的触发器）。|


### <a name="application-schema"></a>应用程序架构

使用这些过程来配置示例。 它们用于适用于标准版中的示例，以及添加审核和全文索引的企业版功能。

|过程|用途|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|如果成员已不在角色的角色添加成员|
|Configuration_ApplyAuditing|将添加审核。 服务器审核适用于标准版数据库;附加的数据库审核将添加用于 enterprise edition。|
|Configuration_ApplyColumnstoreIndexing|将应用到索引的列存储`Sales.OrderLines`和`Sales.InvoiceLines`并相应地重新编制索引。|
|Configuration_ApplyFullTextIndexing|将应用到全文索引`Application.People`， `Sales.Customers`， `Purchasing.Suppliers`，和`Warehouse.StockItems`。 替换`Website.SearchForPeople`， `Website.SearchForSuppliers`， `Website.SearchForCustomers`， `Website.SearchForStockItems`，`Website.SearchForStockItemsByTags`使用全文索引编制的替换过程。|
|Configuration_ApplyPartitioning|将应用到表分区`Sales.CustomerTransactions and `Purchasing.SupplierTransactions 的和排列的索引，以满足。|
|Configuration_ApplyRowLevelSecurity|适用于筛选器客户的行级别安全性的销售区域相关角色。|
|Configuration_ConfigureForEnterpriseEdition|将应用列存储索引、 全文、 内存中，polybase，和分区。|
|Configuration_EnableInMemory|添加由内存优化文件组 （不在 Azure 中工作） 时，将替换`Warehouse.ColdRoomTemperatures`，`Warehouse.VehicleTemperatures`与内存中等效项，并迁移数据时，将重新创建`Website.OrderIDList`， `Website.OrderList`， `Website.OrderLineList`，`Website.SensorDataList`表类型带有内存优化的等效项，将删除并重新创建过程`Website.InvoiceCustomerOrders`， `Website.InsertCustomerOrders`，和`Website.RecordColdRoomTemperatures`使用这些表类型。|
|Configuration_RemoveAuditing|将删除的审核配置。|
|Configuration_RemoveRowLevelSecurity|删除行级别安全性 （这所需的配置对关联的表的更改）。|
|CreateRoleIfNonExistant|如果它尚不存在，则创建的数据库角色。|


### <a name="sequences-schema"></a>序列架构

若要配置数据库中的序列的过程。

|过程|用途|
|-----------------------------|---------------------|
|ReseedAllSequences|调用过程 ReseedSequenceBeyondTableValue 中的所有序列。|
|ReseedSequenceBeyondTableValue|用于在使用相同的序列任何表中重新定位到值之外的下一步序列值。 （如标识列等效项序列，但可能多个表间的 DBCC CHECKIDENT)。|
