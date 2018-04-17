---
title: 使用查询通知 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], query notifications
- rowsets [SQL Server], notifications
- SQL Server Native Client, query notifications
- notifications [SQL Server Native Client]
- query notifications [SQL Server], SQL Server Native Client
- canceling rowset changes
- IRowsetNotify interface
- SQLNCLI, query notifications
- SQL Server Native Client OLE DB provider, query notifications
- consumer notification for rowset changes [SQL Server Native Client]
ms.assetid: 2f906fff-5ed9-4527-9fd3-9c0d27c3dff7
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: faeff47d5daeeb46601020f4e3e31a4c4086386d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-query-notifications"></a>使用查询通知
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中引入了查询通知。 查询通知建立在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的 Service Broker 基础结构之上，并允许在数据发生更改时向应用程序发送通知。 对提供数据库信息的缓存且需要在源数据发生更改时收到通知的应用程序（如 Web 应用程序）而言，以上功能特别有用。  
  
 查询通知使您可以在查询的基础数据发生更改时请求在指定的超时期限内发送通知。 通知请求指定通知选项，其中包括服务名称、消息正文和服务器的超时值。 通知是通过 Service Broker 队列传递的，应用程序可以轮询该队列以获取可用通知。  
  
 查询通知选项字符串的语法为：  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 例如：  
  
 `service=mySSBService;local database=mydb`  
  
 由于应用程序可能在创建通知订阅后终止，因此，通知订阅的生存期比启动它们的进程的生存期长。 订阅将保持有效，如果数据发生更改，则将在创建该订阅时指定的超时期限内发送通知。 通知是通过执行的查询、通知选项和消息正文标识的，将通知的超时值设置为零可以取消该通知。  
  
 只发送一次通知。 对于数据更改的持续通知，必须在处理每个通知之后重新执行查询来创建新的订阅。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端应用程序通常使用收到通知[!INCLUDE[tsql](../../../includes/tsql-md.md)][接收](../../../t-sql/statements/receive-transact-sql.md)命令从与通知选项中指定的服务关联的队列读取通知。  
  
> [!NOTE]  
>  对于需要通知的查询，必须限定其中的表名，例如 `dbo.myTable`。 表名必须用包含两个部分的名称进行限定。 如果使用的名称由三个或四个部分组成，则订阅无效。  
  
 通知基础结构构建在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的队列功能之上。 通常，在服务器上生成的通知是通过这些队列发送的，以便在稍后进行处理。  
  
 若要使用查询通知，服务器上必须存在队列和服务。 使用如下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 可以创建队列和服务：  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  服务必须使用预定义约定 `http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification`，如上所示。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 访问接口  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持使用者通知对行集修改。 使用者在行集修改的每个阶段以及在尝试执行任何更改时接收通知。  
  
> [!NOTE]  
>  传递到与服务器的通知查询**ICommand::Execute**是使用查询通知订阅的唯一有效办法[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。  
  
### <a name="the-dbpropsetsqlserverrowset-property-set"></a>DBPROPSET_SQLSERVERROWSET 属性集  
 若要支持通过 OLE DB 的查询通知[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端将以下新属性添加到 DBPROPSET_SQLSERVERROWSET 属性集。  
  
|名称|类型|Description|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|查询通知保持为活动状态的秒数。<br /><br /> 默认为 432000 秒（5 天）。 最小值为 1 秒，最大值为 2^31-1 秒。|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|通知的消息正文。 消息正文是用户定义的，没有预定义格式。<br /><br /> 默认情况下，该字符串为空。 您可以使用 1 至 2000 个字符指定消息。|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|查询通知选项。 在字符串中以指定了这些*名称*=*值*语法。 用户负责创建服务并从队列中读取通知。<br /><br /> 預設為空字串。|  
  
 无论语句是在用户事务中运行还是以自动提交模式运行，或者无论是提交还是回滚运行语句的事务，将始终提交通知订阅。 根据以下任一无效通知条件激发服务器通知：更改基础数据或架构，或者当达到超时期限时（以先发生者为准）。 激发通知后将立即删除通知注册。 因此，在接收通知时，应用程序必须再次订阅通知，以备进一步更新之用。  
  
 其他连接或线程可以检查通知的目标队列。 例如：  
  
```  
WAITFOR (RECEIVE * FROM MyQueue);   // Where MyQueue is the queue name.   
```  
  
 请注意，选择 * 不从队列中删除该条目，但是接收\*从执行。 如果队列为空，该语句将停止服务器线程。 如果调用时存在队列项，则会立即返回这些队列项；否则调用将一直等待，直到生成队列项为止。  
  
```  
RECEIVE * FROM MyQueue  
```  
  
 如果队列为空，该语句将立即返回空的结果集；否则会返回所有队列通知。  
  
 如果 SSPROP_QP_NOTIFICATION_MSGTEXT 和 SSPROP_QP_NOTIFICATION_OPTIONS 为非 NULL 和非空，当执行其中的每个命令时，将向服务器发送包含上面定义的三个属性的查询通知 TDS 头。 如果其中任一属性为 Null（或空），则不会发送头，并引发 DB_E_ERRORSOCCURRED（或者如果两个属性均标记为可选，则引发 DB_S_ERRORSOCCURRED），同时将状态值设置为 DBPROPSTATUS_BADVALUE。 在执行/准备期间进行验证。 同样，DB_S_ERRORSOCCURED 时引发的查询通知属性进行设置以便连接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之前的版本[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 在这种情况下，状态值为 DBPROPSTATUS_NOTSUPPORTED。  
  
 启动订阅不能保证将成功传递后续消息。 此外，不会检查指定服务名称的有效性。  
  
> [!NOTE]  
>  准备语句永远不会启动订阅；只有执行语句才能实现此目的，并且 OLE DB 核心服务的使用不会影响查询通知。  
  
 有关 DBPROPSET_SQLSERVERROWSET 属性集的详细信息，请参阅[行集属性和行为](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驱动程序  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序还支持通过三个新属性指定给添加的查询通知[SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)和[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)函数：  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
  
 如果 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 和 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS 不为 NULL，每次执行命令时，则不会向服务器发送包含上面定义的三个属性的查询通知 TDS 头。 如果上述两个属性中的任一属性为 Null，则不会发送标头，并返回 SQL_SUCCESS_WITH_INFO。 在时执行验证[SQLPrepare 函数](http://go.microsoft.com/fwlink/?LinkId=59360)， **SqlExecDirect**，和**SqlExecute**，所有的如果属性不是有效的失败。 类似地，当针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 版本设置这些查询通知属性时，执行将失败，并返回 SQL_SUCCESS_WITH_INFO。  
  
> [!NOTE]  
>  准备语句永远不会启动订阅；可以通过执行语句启动订阅。  
  
## <a name="special-cases-and-restrictions"></a>特殊事例和限制  
 通知不支持以下数据类型：  
  
-   **text**  
  
-   **ntext**  
  
-   **image**  
  
 如果针对返回以上任一类型的查询执行通知请求，则立即激发通知，并指明不可能实现通知订阅。  
  
 如果发出批处理或存储过程订阅请求，则会针对批处理或存储过程内执行的每个语句发出单独的订阅请求。 EXECUTE 语句不会注册通知，但是会将通知请求发送到已执行的命令。 如果为批处理，则上下文将适用于已执行的语句，并且应用上述相同规则。  
  
 对于与现有活动订阅具有相同模板、相同参数值、相同通知 ID 和相同传递位置的通知查询，同一用户在相同数据库上下文中再次提交这样的通知查询将续订现有订阅，并重置新指定的超时值。这表示如果针对相同的查询请求通知，则仅发送一个通知。 这将适用于批处理中的重复查询，也适用于存储过程中调用多次的查询。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
