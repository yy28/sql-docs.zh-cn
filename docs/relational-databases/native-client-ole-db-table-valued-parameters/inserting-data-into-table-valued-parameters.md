---
title: "将数据插入到表值参数 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
ms.assetid: 9c1a3234-4675-40d3-b473-8df06208f880
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f40d26c1e3d44e90375907845ea5ee60ef414fb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="inserting-data-into-table-valued-parameters"></a>向表值参数中插入数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持的使用者，以指定表值参数行数据的两个模型： 推送模型和请求模型。 一个示例，演示拉取模型是可用;请参阅[SQL Server 数据编程示例](http://msftdpprodsamples.codeplex.com/)。  
  
> [!NOTE]  
>  表值参数列要么必须在所有行中具有非默认值，要么必须在所有行中具有默认值。 不能在某些行中具有默认值，而在其他行中不具有默认值。 因此，在表值参数绑定中，表值参数行集列数据仅允许状态值 DBSTATUS_S_ISNULL 和 DBSTATUS_S_OK。 DBSTATUS_S_DEFAULT 将导致失败，而绑定的状态值将设置为 DBSTATUS_E_BADSTATUS。  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>推送模型（在内存中加载所有表值参数数据）  
 推送模型是类似于使用的参数集 （即，在 ICommand::Execute DBPARAMS 参数）。 如果使用表值参数行集对象时不进行 IRowset 接口的自定义实现，则仅使用推送模型。 当表值参数行集中的行数较少且预计不会给应用程序带来过量内存压力时，建议使用推送模型。 这比请求模型更简单，因为它向使用者应用程序要求的功能不会超过典型 OLE DB 应用程序中当前常用的功能。  
  
 使用者应在执行命令之前向访问接口提供所有表值参数数据。 为提供数据，使用者为每个表值参数填充一个表值参数行集对象。 表值参数行集对象显示行集 Insert、Set 和 Delete 操作，使用者将使用这些操作来操作表值参数数据。 访问接口在执行时将从该表值参数行集对象中提取数据。  
  
 当向使用者提供表值参数行集对象时，使用者可以将其作为行集对象处理。 使用者可以使用 IColumnsInfo::GetColumnInfo 或 IColumnsRowset::GetColumnsRowset 接口方法获取每个列 （类型、 最大长度、 精度和缩放） 的类型信息。 然后，使用者创建取值函数，以便为数据指定绑定。 下一步是将数据行插入表值参数行集。 这可以通过使用 IRowsetChange::InsertRow 完成。 IRowsetChange::SetData 或 IRowsetChange::DeleteRows 还可在表值参数行集对象上如果必须处理的数据。 表值参数行集对象将进行引用计数，这与流对象类似。  
  
 如果使用 IColumnsRowset::GetColumnsRowset，则将对 irowset:: Getnextrows、 irowset:: Getdata 和 irowset:: Releaserows 方法生成的列的行集对象上的后续调用。  
  
 后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口开始执行该命令，将从此表值参数行集对象提取的表值参数值，并将其发送到服务器。  
  
 推送模型对于使用者的工作量要求最少，但占用的内存高于请求模型，原因在于在执行时所有表值参数数据都必须位于内存中。  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>请求模型（从使用者按需获得表值参数数据）  
 请求模型用于两种应用场景：  
  
-   使行成为流数据。  
  
-   如果其他访问接口中的行集正用作表值参数值。  
  
 在请求模型中，使用者按需为访问接口提供数据。 如果应用程序具有许多数据插入操作，并且内存中的表值参数行集数据将导致过量的内存访问，则使用此方法。 如果使用多个 OLE DB 访问接口，则借助于使用者请求模型，使用者可以将任何行集对象作为表值参数值提供。  
  
 为了使用请求模型，使用者必须提供其自己的对于行集对象的实现。 使用表值参数行集 (CLSID_ROWSET_TVP) 拉取模式，使用者时，需要聚合表值参数行集公开的对象，该提供程序通过 ITableDefinitionWithConstraints::CreateTableWithConstraints 方法或 IOpenRowset::OpenRowset 方法。 使用者对象应只覆盖 IRowset 接口实现。 您必须覆盖以下函数：  
  
-   IRowset::GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset::GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset::RestartPosition  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将一次从使用者行集对象中读取一行或多行，以便在表值参数中支持流行为。 例如，用户可能在磁盘上（而非内存中）具有表值参数行集数据，当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口要求时，可能实现从磁盘读取数据的功能。  
  
 使用者将通信到其数据格式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序对表值参数行集对象使用 IAccessor::CreateAccessor。 当从使用者缓冲区读取数据时，访问接口将验证所有可写入和非默认列是否至少可用于一个取值函数句柄，并使用相应的句柄来读取列数据。 若要避免多义性，则应将表值参数行集列和绑定之间的一一对应关系。 与同一列的重复绑定将导致错误。 此外，每个访问器需要具有*iOrdinal* DBBindings 的序列中的成员。 为每个行，访问器数将有任意多个 irowset:: Getdata 调用，并且调用的顺序将按顺序排列的*iOrdinal*从到更高版本较低的值的值。  
  
 访问接口应实现由表值参数行集对象显示的大多数接口。 使用者将实现具有最小接口 (IRowset) 的行集对象。 由于盲聚合 (blind aggregation)，因此，表值参数行集对象将实现剩下的所必需的行集对象接口。  
  
 对于任何其他行集对象（如对于任何 OLE DB 访问接口获得的行集对象），使用者提供的行集必须按照 OLE DB 规范要求实现所有必需的行集对象接口。  
  
 在执行时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将回调行集对象以提取行并读取列数据。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
