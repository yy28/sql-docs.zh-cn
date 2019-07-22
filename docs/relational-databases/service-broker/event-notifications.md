---
title: 事件通知 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications, about
- events [SQL Server], notifications
ms.assetid: 4da73ca1-6c06-4e96-8ab8-2ecba30b6c86
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f5433d6082f2860805368f636383eb2e17959e77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048858"
---
# <a name="event-notifications"></a>事件通知
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  事件通知将有关事件的信息发送给 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服务。 执行事件通知可对各种 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据定义语言 (DDL) 语句和 SQL 跟踪事件做出响应，其方法是将这些事件的相关信息发送到 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服务。  
  
 事件通知可以用来执行以下操作：  
  
-   记录和检索发生在数据库上的更改或活动。  
  
-   执行操作以异步方式而不是同步方式响应事件。  
  
 可以将事件通知用作替代 DDL 触发器和 SQL 跟踪的编程方法。  
  
## <a name="event-notifications-benefits"></a>事件通知优点  
 事件通知在事务范围以外异步运行。 因此，与 DDL 触发器不同，事件通知可以用于数据库应用程序中以响应事件而无需使用中间事务定义的任何资源。  
  
 与 SQL 跟踪不同，事件通知可用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例内部执行操作以响应 SQL 跟踪事件。  
  
 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起运行的应用程序可以使用事件数据来跟踪进度并做出决策。 例如，在 `ALTER TABLE` 示例数据库中，每当发出一条 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 语句时，以下事件通知都会将一条通知发送给特定的服务。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE '//Adventure-Works.com/ArchiveService' ,  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
## <a name="event-notifications-concepts"></a>事件通知概念  
 创建事件通知时，将会在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 实例和指定的目标服务之间打开一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会话。 通常会话保持为打开状态，只要事件通知作为一个对象存在于服务器实例中。 在某些出错情况下，会话可以在删除事件通知之前关闭。 这些会话从不在事件通知之间共享。 每个事件通知都有自己的排他会话。 显式结束会话将阻止目标服务接收更多消息，下一次事件通知激发时，会话将不会重新打开。  
  
 事件信息作为 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 类型的变量传递给 **xml** 服务，它提供了有关事件的发生时间、受影响的数据库对象、涉及的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理语句的信息以及其他信息。 有关事件通知生成的 XML 架构的详细信息，请参阅 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)。  
  
### <a name="event-notifications-vs-triggers"></a>事件通知与触发器  
 下表对触发器和事件通知进行了比较。  
  
|触发器|事件通知|  
|--------------|-------------------------|  
|DML 触发器响应数据操作语言 (DML) 事件。 DDL 触发器响应数据定义语言 (DDL) 事件。|事件通知响应 DDL 事件和部分 SQL 跟踪事件。|  
|触发器可以运行 Transact-SQL 或公共语言运行时 (CLR) 托管代码。|事件通知不运行代码， 而是向 Service Broker 服务发送 **xml** 消息。|  
|触发器在导致其激发的事务的作用域内同步处理。|事件通知可以异步处理，并且不在导致其激发的事务的作用域内运行。|  
|触发器的使用者与导致触发器激发的事件紧密结合。|事件通知的使用者与导致事件通知激发的事件相分离。|  
|触发器必须在本地服务器上处理。|事件通知可以在远程服务器上处理。|  
|触发器可以回滚。|事件通知不能回滚。|  
|DML 触发器名称的架构范围。 DDL 触发器名称是数据库范围或服务器范围的。|事件通知的名称由服务器或数据库限定范围。 QUEUE_ACTIVATION 事件的事件通知限定于一个特定的队列。|  
|DML 触发器与其应用的表属于相同的所有者。|队列上的事件通知的所有者可以与所应用对象的所有者不同。|  
|触发器支持 EXECUTE AS 子句。|事件通知不支持 EXECUTE AS 子句。|  
|可以使用 EVENTDATA 函数（返回 **xml** 数据类型）捕获 DDL 触发器事件信息。|事件通知向 Service Broker 服务发送 **xml** 事件信息。 该信息被格式化为与 EVENTDATA 函数的架构相同的架构。|  
|有关触发器的元数据可在 **sys.triggers** 和 **sys.server_triggers** 目录视图中找到。|有关事件通知的元数据可在 **sys.event_notifications** 和 **sys.server_event_notifications** 目录视图中找到。|  
  
### <a name="event-notifications-vs-sql-trace"></a>事件通知与SQL 跟踪  
 下表对使用事件通知和 SQL 跟踪监视服务器事件进行比较和对照。  
  
|SQL 跟踪|事件通知|  
|---------------|-------------------------|  
|SQL 跟踪不会对与事务关联的性能造成负面影响。 打包数据很有效。|创建 XML 格式的事件数据和发送事件通知会对性能造成关联的负面影响。|  
|SQL 跟踪可以监视任何跟踪事件类。|事件通知可以监视部分跟踪事件类和所有数据定义语言 (DDL) 事件。|  
|您可以自定义在跟踪事件中生成哪些数据列。|由事件通知返回的 XML 格式的事件数据架构是固定的。|  
|无论是否回滚 DDL 语句，都将始终生成 DDL 生成的跟踪事件。|如果回滚相应 DDL 语句中的事件，则事件通知不会触发。|  
|管理跟踪事件数据的中间流涉及填充和管理跟踪文件或跟踪表。|事件通知数据的中间管理将通过 Service Broker 队列自动执行。|  
|每次重新启动服务器时，都必须重新启动跟踪。|注册之后，事件通知将保持在服务器循环中，并进行事务处理。|  
|启动之后，无法控制触发跟踪。 停止时间和筛选时间可用于指定何时启动。 可以通过轮询相应的跟踪文件访问跟踪。|通过对接收事件通知生成的消息的队列使用 WAITFOR 语句可以控制事件通知。 可以通过轮询队列访问它们。|  
|ALTER TRACE 是创建跟踪所需的最低权限。 在相应计算机上创建跟踪文件也需要该权限。|最低权限取决于要创建的事件通知的类型。 相应队列还需要 RECEIVE 权限。|  
|可以远程接收跟踪。|可以远程接收事件通知。|  
|可以使用系统存储过程实现跟踪事件。|通过组合使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssSB](../../includes/sssb-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] 语句实现事件通知。|  
|通过查询相应的跟踪表、分析跟踪文件或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) TraceReader 类能够以编程方式访问跟踪事件数据。|可以通过对 XML 格式的事件数据执行 XQuery 或使用 SMO 事件类，以编程方式访问事件数据。|  
  
## <a name="event-notification-tasks"></a>事件通知任务  
  
|任务|主题|  
|----------|-----------|  
|介绍如何创建和实现事件通知。|[实现事件通知](../../relational-databases/service-broker/implement-event-notifications.md)|  
|介绍如何为发送消息到远程服务器中 Service Broker 的事件通知配置 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对话安全模式。|[配置事件通知的对话安全模式](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)|  
|介绍如何返回有关事件通知的信息。|[获取有关事件通知的信息](../../relational-databases/service-broker/get-information-about-event-notifications.md)|  
  
## <a name="see-also"></a>另请参阅  
 [DDL 触发器](../../relational-databases/triggers/ddl-triggers.md)   
 [DML 触发器](../../relational-databases/triggers/dml-triggers.md)   
 [SQL 跟踪](../../relational-databases/sql-trace/sql-trace.md)  
  
  
