---
title: 使用查询通知 |Microsoft Docs
description: 使用 SQL Server 的 OLE DB 驱动程序中的查询通知
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], query notifications
- rowsets [SQL Server], notifications
- OLE DB Driver for SQL Server, query notifications
- notifications [OLE DB Driver for SQL Server]
- query notifications [SQL Server], OLE DB Driver for SQL Server
- canceling rowset changes
- IRowsetNotify interface
- MSOLEDBSQL, query notifications
- OLE DB Driver for SQL Server, query notifications
- consumer notification for rowset changes [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 29aaab523b3a754c65b1b7a0312ceb5ea122f2d3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419316"
---
# <a name="working-with-query-notifications"></a>使用查询通知

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

查询通知在中引入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , 并 OLE DB SQL Server 的驱动程序中。 查询通知建立在 SQL Server 2005 (9.x) 中引入的 SQL Service Broker 基础结构之上，并允许在数据发生更改时向应用程序发送通知。 对提供数据库信息的缓存且需要在源数据发生更改时收到通知的应用程序（如 Web 应用程序）而言，以上功能特别有用。

通过使用查询通知, 可以在查询的基础数据发生更改时, 在指定的超时期限内请求通知。 请求指定通知选项，其中包括服务名称、消息正文和服务器的超时值。 通知是通过 Service Broker 队列传递的，应用程序可轮询该队列来获取可用通知。

查询通知选项字符串的语法为：

`service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`

 例如：

`service=mySSBService;local database=mydb`

通知订阅长于启动它们的进程。 这是因为应用程序可以创建通知订阅, 然后终止。 订阅保持有效，如果数据发生更改，则在创建该订阅时指定的超时期限内发送通知。 通知由执行的查询、通知选项和消息文本标识。 可以通过将其超时值设置为零来取消它。

只发送一次通知。 若要持续通知数据更改, 请在处理每个通知后, 通过重新执行查询来创建新的订阅。

SQL Server 应用程序 OLE DB 驱动程序通常使用[!INCLUDE[tsql](../../../includes/tsql-md.md)] [RECEIVE](../../../t-sql/statements/receive-transact-sql.md)命令接收通知。 它使用此命令从与通知选项中指定的服务关联的队列中读取通知。

> [!NOTE]
> 对于需要通知的查询，必须限定其中的表名。 例如， `dbo.myTable`。 表名必须用包含两个部分的名称进行限定。 如果使用的名称由三个或四个部分组成，则订阅无效。

通知基础结构构建在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的队列功能之上。 通常，服务器上生成的通知是通过这些队列发送的，以便稍后进行处理。

若要使用查询通知，服务器上必须存在队列和服务。 可以使用[!INCLUDE[tsql](../../../includes/tsql-md.md)]命令创建这些内容, 如下所示:

```sql
CREATE QUEUE myQueue
CREATE SERVICE myService ON QUEUE myQueue
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])
```

> [!NOTE]
> 服务必须使用预定义约定，如上所示。

## <a name="ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序

SQL Server 的 OLE DB 驱动程序在行集修改时支持使用者通知。 使用者在行集修改的每个阶段以及在尝试执行任何更改时接收通知。

> [!NOTE]
> 使用 ICommand::Execute 向服务器传递通知查询是向适用于 SQL Server 的 OLE DB 驱动程序订阅查询通知的唯一有效方式  。

### <a name="dbpropsetsqlserverrowset-property-set"></a>DBPROPSET_SQLSERVERROWSET 属性集

为通过 OLE DB 支持查询通知，OLE DB Driver for SQL Server 向 `DBPROPSET_SQLSERVERROWSET` 属性集添加了以下新属性。

|“属性”|类型|描述|
|----------|----------|-----------------|
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|查询通知保持为活动状态的秒数。<br /><br /> 默认为 432000 秒（5 天）。 最小值为 1 秒，最大值为 2^31-1 秒。|
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|通知的消息正文。 此消息是用户定义的，没有预定义格式。<br /><br /> 默认情况下，该字符串为空。 使用1到2000个字符指定一条消息。|
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|查询通知选项。 采用 name=value 语法以字符串形式指定这些内容   。 用户负责创建服务并从队列中读取通知。<br /><br /> 默认值为空字符串。|

始终提交通知订阅。 无论语句是在用户事务中运行还是在自动提交中运行, 或者在运行该语句的事务是否已提交或回滚, 都将发生这种情况。 根据以下任一无效通知条件激发服务器通知：更改基础数据或架构，或者当达到超时期限时（以先发生者为准）。 

激发通知后将立即删除通知注册。 因此，在接收通知时，如果你想要获取进一步的更新，应用程序必须再次订阅通知。

其他连接或线程可以检查通知的目标队列。 例如：

```sql
WAITFOR (RECEIVE * FROM MyQueue); -- Where MyQueue is the queue name.
```

> [!NOTE]
> `SELECT *`不会从队列中删除该项。 不过, `RECEIVE * FROM`确实如此。 如果队列为空，该语句将停止服务器线程。 如果在调用时有队列项, 则它们将立即返回。 否则, 调用将等待, 直到排队条目。

```sql
RECEIVE * FROM MyQueue
```

如果队列为空, 则此语句立即返回空的结果集。 否则, 它将返回所有队列通知。

如果`SSPROP_QP_NOTIFICATION_MSGTEXT` 和`SSPROP_QP_NOTIFICATION_OPTIONS`不是 null 且不为空, 则会向服务器发送包含上面定义的三个属性的查询通知 TDS 头。 每次执行命令时都会发生这种情况。 如果其中任何一个为空 (或为空), 则不会发送`DB_E_ERRORSOCCURRED`标头并引发`DB_S_ERRORSOCCURRED` (如果这些属性都标记为可选, 则会引发此标头)。 然后, 将状态值设置为`DBPROPSTATUS_BADVALUE`。 执行和准备时进行验证。 类似地，当设置查询通知属性以连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本时，将引发 `DB_S_ERRORSOCCURED`。 在本例中, status 值为`DBPROPSTATUS_NOTSUPPORTED`。

启动订阅不能保证将成功传递后续消息。 此外，不检查指定服务名称的有效性。

> [!NOTE]
> 准备语句永远不会启动订阅。 只有语句执行才能实现。 查询通知并不会影响 OLE DB 核心服务的使用。

有关属性集的`DBPROPSET_SQLSERVERROWSET`详细信息, 请参阅[行集属性和行为](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)。

## <a name="see-also"></a>另请参阅

[适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)
