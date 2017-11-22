---
title: "开始会话计时器 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONVERSATION
- BEGIN_CONVERSATION_TSQL
- TIMER_TSQL
- TIMER
- CONVERSATION TIMER
- CONVERSATION_TIMER_TSQL
- BEGIN CONVERSATION TIMER
- BEGIN_CONVERSATION_TIMER_TSQL
- CONVERSATION_TSQL
- BEGIN CONVERSATION
dev_langs: TSQL
helpviewer_keywords:
- BEGIN CONVERSATION TIMER statement
- DialogTimer message
- dialogs [Service Broker], beginning
- timeouts [Service Broker]
- timer messages [Service Broker]
- conversations [Service Broker], timers
- starting timers [Service Broker]
- http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer message
ms.assetid: 98e49b3f-a38f-4180-8171-fa9cb30db4cb
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3772f81727b60f5c7932671fa10f5ca6454047c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="begin-conversation-timer-transact-sql"></a>BEGIN CONVERSATION TIMER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  启动计时器。 当超时到期时，[!INCLUDE[ssSB](../../includes/sssb-md.md)]放入类型的消息的`http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`会话的本地队列上。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
BEGIN CONVERSATION TIMER ( conversation_handle )  
   TIMEOUT = timeout   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 开始会话定时器**(***conversation_handle***)**  
 指定要计时的会话。 *Conversation_handle*的类型必须为**uniqueidentifier**。  
  
 TIMEOUT  
 指定在将消息放入队列之前要等待的时间，以秒为单位。  
  
## <a name="remarks"></a>注释  
 会话计时器为应用程序提供了一种方式，可以在指定时间后接收与某个会话有关的消息。 如果在计时器过期前对会话调用 BEGIN CONVERSATION TIMER，可将超时设置为新值。 与会话生存期不同，会话双方的会话计时器彼此独立。 **DialogTimer**消息到达本地队列上而不会影响会话的远程端。 因此，应用程序可以将计时器消息用于任何目的。  
  
 例如，可以使用会话计时器避免应用程序过久地等待过期响应。 如果希望应用程序在 30 秒内完成对话，则可将对话的会话计时器设置为 60 秒（30 秒加 30 秒的宽限期）。 如果对话 60 秒后仍处于打开状态，则应用程序将收到一条关于该对话队列的超时消息。  
  
 此外，应用程序可以使用会话计时器请求在特定时间进行激活。 例如，可以创建一个服务，每隔几分钟报告活动连接数；或者创建一种服务，每天晚上报告未清的采购订单。 服务设置一个会话计时器，以在所需的时间; 过期当计时器到期时，[!INCLUDE[ssSB](../../includes/sssb-md.md)]发送**DialogTimer**消息。 **DialogTimer**消息原因[!INCLUDE[ssSB](../../includes/sssb-md.md)]启动激活存储过程的队列。 该存储过程将向远程服务发送一条消息，并重新启动会话计时器。  
  
 BEGIN CONVERSATION TIMER 在用户定义函数中无效。  
  
## <a name="permissions"></a>Permissions  
 将会话定时器设置默认值为会话的成员的服务具有发送权限的用户权限**sysadmin**固定服务器角色和成员的**db_owner**固定的数据库角色。  
  
## <a name="examples"></a>示例  
 以下示例为由 `@dialog_handle` 标识的对话设置两分钟的超时。  
  
```  
-- @dialog_handle is of type uniqueidentifier and  
-- contains a valid conversation handle.  
  
BEGIN CONVERSATION TIMER (@dialog_handle)  
TIMEOUT = 120 ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN DIALOG CONVERSATION &#40;Transact SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;Transact SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [接收 &#40;Transact SQL &#41;](../../t-sql/statements/receive-transact-sql.md)  
  
  
