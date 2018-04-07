---
title: 使用多个活动结果集 (MARS) |Microsoft 文档
description: 使用多个活动的结果集 (MARS)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, MARS
- MSOLEDBSQL, MARS
- data access [OLE DB Driver for SQL Server], MARS
- Multiple Active Result Sets
- OLE DB Driver for SQL Server, MARS
- MARS [SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 39950e9e23e0f77de977a0f0d276fdf8db6f1259
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="using-multiple-active-result-sets-mars"></a>使用多个活动的结果集 (MARS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入了支持多个活动结果集 (MARS) 访问的应用程序中[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的早期版本中，数据库应用程序无法在单个连接上保持多个活动语句。 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认结果集时，应用程序必须先处理或取消从某一批处理生成的所有结果集，然后才能对该连接执行任何其他批处理。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入了新的连接属性，该属性允许应用程序在每个连接上使用多个待定请求，具体而言，每个连接可以具有多个活动的默认结果集。  
  
 MARS 通过以下新功能简化了应用程序设计：  
  
-   应用程序可以同时打开多个默认结果集，并且交错读取它们。  
  
-   应用程序可以在默认结果集打开的同时执行其他语句（例如 INSERT、UPDATE、DELETE 和存储过程调用）。  
  
 下列指南对使用 MARS 的应用程序很有帮助：  
  
-   默认结果集应该用于使用单个 SQL 语句（SELECT、带 OUTPUT 的 DML、RECEIVE、READ TEXT 等）生成的短期或较小结果集。  
  
-   服务器游标应该用于使用单个 SQL 语句生成的长期或较大结果集。  
  
-   对于过程请求（不论它们是否返回结果）以及返回多个结果的批处理，应始终读取到它们的结果的末尾。  
  
-   尽可能使用 API 调用（而不是 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句）更改连接属性和管理事务。  
  
-   在 MARS 中，有多个批处理并发运行时禁止会话范围内的模拟。  
  
> [!NOTE]  
>  默认情况下，不启用 MARS 功能。 若要连接到时使用 MARS[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 OLE DB 驱动程序的 SQL Server，你必须专门启用其连接字符串中。 有关详细信息，请参阅本主题中的更高版本的 SQL Server 部分，用于 OLE DB 驱动程序。  
  
 OLE DB 驱动程序的 SQL Server 不限制在连接上的活动语句数。  
  
 不需要同时执行多个多语句批处理或存储过程的典型应用程序将受益于 MARS，且无需了解如何实现 MARS。 不过，具有较复杂要求的应用程序确实需要考虑到这一点。  
  
 MARS 支持在单一连接中交错执行多个请求。 即：它允许运行批处理，并且在执行过程中还允许执行其他请求。 不过请注意，MARS 是从交错执行而不是从并行执行的角度定义的。  
  
 MARS 基础结构允许以交错方式执行多个批处理，尽管只能在定义完善的时间点切换执行。 此外，多数语句必须在同一批处理内以原子方式运行。 返回到客户端，有时称为行语句*产生点*，允许交错在完成之前执行，而行发送到客户端，例如：  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 作为存储过程或批处理的一部分执行的任何其他语句必须运行完毕，之后才能切换到执行其他 MARS 请求。  
  
 多个批处理交错执行的确切方式受若干因素影响，很难预测包含收获点的多个批处理中的命令的确切执行顺序。 注意避免交错执行此类复杂批处理所产生的意外负面影响。  
  
 要避免这些问题，可使用 API 调用而不是 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句来管理连接状态（SET、USE）和事务（BEGIN TRAN、COMMIT、ROLLBACK），方法是不在同样包含收获点的多语句批处理中包括这些语句，以及通过使用或取消所有结果来顺序执行此类批处理。  
  
> [!NOTE]  
>  启用 MARS 时，启动手动或隐式事务的批处理或存储过程必须完成该事务，之后批处理才能退出。 如果不是这样，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将在批处理完成时回滚该事务所做的所有更改。 这种事务由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 作为批范围的事务管理。 这是 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 新引入的事务类型，用于在启用 MARS 时支持使用功能良好的现有存储过程。 有关批处理范围事务的详细信息，请参阅[Transaction 语句&#40;TRANSACT-SQL&#41;](../../../t-sql/statements/statements.md)。  
  
 使用 MARS 从 ADO 的示例，请参阅[与 OLE DB 驱动程序的 SQL Server 使用 ADO](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。  
  
## <a name="in-memory-oltp"></a>内存中 OLTP  
 内存中 OLTP 支持 MARS 使用查询和本机编译存储的过程。 MARS 允许将从而无需完全检索每个结果才能发送请求以从新的结果集中提取行集的多个查询的请求数据。 若要成功读取从多个打开的结果集必须使用 MARS 启用连接。  
  
 默认情况下禁用 MARS，因此你必须通过添加显式启用`MultipleActiveResultSets=True`到连接字符串。 下面的示例演示如何连接到 SQL Server 的实例并指定启用了 MARS:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 MARS 使用内存中 OLTP 是实质上是 MARS 相同 SQL 引擎的其余部分。 以下列出使用 MARS，在内存优化表和本机编译的存储的过程的差异。  
  
 **MARS 和内存优化表**  
  
 当使用 MARS 启用连接时，基于磁盘和内存优化表之间的差异如下：  
  
-   两个语句可以修改相同的目标对象中的数据，但如果这两个用户尝试修改同一记录写入-写入冲突将导致新的操作失败。 但是，如果这两个操作修改不同的记录，操作将会成功。  
  
-   每个语句在快照隔离级别下运行，因此新的操作无法看到由现有语句所做的更改。 即使在同一事务下执行并发语句的 SQL 引擎创建批处理范围事务为每个语句，相互隔离。 但是，批处理范围事务仍绑定在一起以便回滚一个批处理范围事务会影响同一批处理中的其他计算机。  
  
-   在用户事务中不允许 DDL 操作，因此它们将立即失败。  
  
 **MARS 和本机编译存储的过程**  
  
 本机编译存储的过程中启用 MARS 连接可以运行，并仅在遇到 yield 点时，才可以产生于另一个语句的执行。 Yield 点要求的 SELECT 语句，这是本机编译的存储过程可以生成执行的另一个语句中的唯一语句。 如果 SELECT 语句不存在它不会产生任何过程中，它将完成之前运行其他语句开始。  
  
 **MARS 和内存中 OLTP 事务**  
  
 语句块和交错的原子块所做的更改是相互隔离的。 例如，如果一个语句或原子块进行某些更改，然后生成到另一个语句执行新语句将不会看到第一个语句所做的更改。 此外，当第一条语句重新开始执行，不会看到任何其他语句所做的任何更改。 语句将仅查看完成并提交该语句开始前的更改。  
  
 可以使用 BEGIN TRANSACTION 语句在当前用户事务中启动新用户事务 – 这是支持仅在互操作模式下，因此，只能从 T-SQL 的语句，调用 BEGIN TRANSACTION，不从在本机编译存储过程。你可以创建一个保存点在事务使用 SAVE TRANSACTION 或对事务的 API 调用中。回滚到保存点 Save(save_point_name)。 此功能同时会启用仅从 T-SQL 语句，并不是从在本机编译存储的过程。  
  
 **MARS 和列存储索引**  
  
 SQL Server （从 2016年开始） 与列存储索引支持 MARS。 SQL Server 2014 将 MARS 用于具有列存储索引的表的只读连接。    但是，SQL Server 2014 不支持将 MARS 用于具有列存储索引的表中的并发数据操作语言 (DML) 操作。 当发生这种情况时，SQL Server 将终止连接，中止事务。   SQL Server 2012 具有只读列存储索引和 MARS 不适用于它们。  
  
## <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序  
 SQL Server 的 OLE DB 驱动程序支持 SSPROP_INIT_MARSCONNECTION 数据源初始化属性，用于实现 dbpropset_sqlserverdbinit 限设置的属性中添加了 MARS。 此外，新的连接字符串关键字， **MarsConn**，如已添加。 它接受**true**或**false**值;**false**是默认设置。  
  
 数据源属性 DBPROP_MULTIPLECONNECTIONS 默认为 VARIANT_TRUE。 这意味着访问接口将生成多个连接以支持多个并发命令和行集对象。 启用 MARS 后，OLE DB 驱动程序的 SQL Server 可以在单个连接上支持多个命令和行集对象，因此 MULTIPLE_CONNECTIONS 默认设置为 VARIANT_FALSE。  
  
 有关 dbpropset_sqlserverdbinit 限属性集对所做的增强功能的详细信息，请参阅[初始化和授权属性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
### <a name="ole-db-driver-for-sql-server-example"></a>有关 SQL Server 示例的 OLE DB 驱动程序  
 在此示例中，创建数据源对象时使用的 SQL Server OLE DB 驱动程序并使用在创建会话对象之前设置 dbpropset_sqlserverdbinit 限属性启用 MARS。  
  
```  
#include <msoledbsql.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  

  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 
  
  
