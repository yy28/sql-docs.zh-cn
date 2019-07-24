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
ms.openlocfilehash: 5b563099b161fa9b55a72820edd3411a4c72b4fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988728"
---
# <a name="working-with-query-notifications"></a>使用查询通知

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

查询通知在中引入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , 并 OLE DB SQL Server 的驱动程序中。 查询通知建立在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的 Service Broker 基础结构之上，并允许在数据发生更改时向应用程序发送通知。 对提供数据库信息的缓存且需要在源数据发生更改时收到通知的应用程序（如 Web 应用程序）而言，以上功能特别有用。

查询通知使您可以在查询的基础数据发生更改时请求在指定的超时期限内发送通知。 通知请求指定通知选项，其中包括服务名称、消息正文和服务器的超时值。 通知是通过 Service Broker 队列传递的，应用程序可以轮询该队列以获取可用通知。

查询通知选项字符串的语法为：

`service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`

 例如：

`service=mySSBService;local database=mydb`

由于应用程序可能在创建通知订阅后终止，因此，通知订阅的生存期比启动它们的进程的生存期长。 订阅将保持有效，如果数据发生更改，则将在创建该订阅时指定的超时期限内发送通知。 通知是通过执行的查询、通知选项和消息文本标识的；如果将通知的超时值设置为零，可以取消通知。

只发送一次通知。 对于数据更改的持续通知，必须在处理每个通知之后重新执行查询来创建新的订阅。

适用于 SQL Server 的 OLE DB 驱动程序应用程序通常使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] [RECEIVE](../../../t-sql/statements/receive-transact-sql.md) 命令接收通知，以便读取与通知选项中指定的服务相关联的队列中的通知。

> [!NOTE]
> 对于需要通知的查询，必须限定其中的表名，例如 `dbo.myTable`。 表名必须用包含两个部分的名称进行限定。 如果使用的名称由三个或四个部分组成，则订阅无效。

通知基础结构构建在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的队列功能之上。 通常，在服务器上生成的通知是通过这些队列发送的，以便在稍后进行处理。

若要使用查询通知，服务器上必须存在队列和服务。 使用如下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 可以创建队列和服务：

```sql
CREATE QUEUE myQueue
CREATE SERVICE myService ON QUEUE myQueue
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])
```

> [!NOTE]
> 服务必须使用预定义协定，如上所示。

## <a name="ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序

SQL Server 的 OLE DB 驱动程序在行集修改时支持使用者通知。 使用者在行集修改的每个阶段以及在尝试执行任何更改时接收通知。

> [!NOTE]
> 使用 ICommand::Execute 向服务器传递通知查询是向适用于 SQL Server 的 OLE DB 驱动程序订阅查询通知的唯一有效方式  。

### <a name="the-dbpropsetsqlserverrowset-property-set"></a>DBPROPSET_SQLSERVERROWSET 属性集

为通过 OLE DB 支持查询通知，适用于 SQL Server 的 OLE DB 驱动程序向 DBPROPSET_SQLSERVERROWSET 属性集添加了以下新属性。

|“属性”|类型|描述|
|----------|----------|-----------------|
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|查询通知保持为活动状态的秒数。<br /><br /> 默认为 432000 秒（5 天）。 最小值为 1 秒，最大值为 2^31-1 秒。|
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|通知的消息正文。 消息正文是用户定义的，没有预定义格式。<br /><br /> 默认情况下，该字符串为空。 您可以使用 1 至 2000 个字符指定消息。|
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|查询通知选项。 采用 name=value 语法以字符串形式指定这些内容   。 用户负责创建服务并从队列中读取通知。<br /><br /> 默认值为空字符串。|

无论语句是在用户事务中运行还是以自动提交模式运行，或者无论是提交还是回滚运行语句的事务，将始终提交通知订阅。 根据以下任一无效通知条件激发服务器通知：更改基础数据或架构，或者当达到超时期限时（以先发生者为准）。 激发通知后将立即删除通知注册。 因此，在接收通知时，应用程序必须再次订阅通知，以备进一步更新之用。

其他连接或线程可以检查通知的目标队列。 例如：

```sql
WAITFOR (RECEIVE * FROM MyQueue); -- Where MyQueue is the queue name.
```

> [!NOTE]
> SELECT * 不会从 Queue 中删除条目，但 RECEIVE \* FROM 却会。 如果队列为空，该语句将停止服务器线程。 如果调用时存在队列项，则会立即返回这些队列项；否则调用将一直等待，直到生成队列项为止。

```sql
RECEIVE * FROM MyQueue
```

如果队列为空，该语句将立即返回空的结果集；否则会返回所有队列通知。

如果 SSPROP_QP_NOTIFICATION_MSGTEXT 和 SSPROP_QP_NOTIFICATION_OPTIONS 为非 NULL 和非空，当执行其中的每个命令时，将向服务器发送包含上面定义的三个属性的查询通知 TDS 头。 如果其中任一属性为 Null（或空），则不会发送头，并引发 DB_E_ERRORSOCCURRED（或者如果两个属性均标记为可选，则引发 DB_S_ERRORSOCCURRED），同时将状态值设置为 DBPROPSTATUS_BADVALUE。 在执行/准备期间进行验证。 类似地，当设置查询通知属性以便连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本时，将引发 DB_S_ERRORSOCCURED。 在这种情况下，状态值为 DBPROPSTATUS_NOTSUPPORTED。

启动订阅不能保证将成功传递后续消息。 此外，不会检查指定服务名称的有效性。

> [!NOTE]
> 准备语句永远不会启动订阅；只有执行语句才能实现此目的，并且 OLE DB 核心服务的使用不会影响查询通知。

有关 DBPROPSET_SQLSERVERROWSET 属性集的详细信息, 请参阅[行集属性和行为](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)。

## <a name="see-also"></a>另请参阅

[适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)
