---
title: "END CONVERSATION (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- END DIALOG
- END CONVERSATION
- END_DIALOG_TSQL
- END_CONVERSATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [Service Broker], conversations
- dialogs [Service Broker], ending
- closing conversations
- END CONVERSATION statement
- conversations [Service Broker], ending
- ending conversations [SQL Server]
ms.assetid: 4415a126-cd22-4a5e-b84a-d8c68515c83b
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60923cb3ad494aacc9d39653a2462da3fe27b46a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="end-conversation-transact-sql"></a>END CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  结束现有会话中的某一方。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
END CONVERSATION conversation_handle  
   [   [ WITH ERROR = failure_code DESCRIPTION = 'failure_text' ]  
     | [ WITH CLEANUP ]  
    ]  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *conversation_handle*  
 要结束的会话的会话句柄。  
  
 出现错误 =*failure_code*  
 是错误代码。 *Failure_code*属于类型**int**。失败代码是用户定义代码，包含在发送给会话另一方的错误消息中。 失败代码必须大于 0。  
  
 说明 =*failure_text*  
 是错误消息。 *Failure_text*属于类型**nvarchar(3000)**。 失败文本是用户定义文本，包含在发送给会话另一方的错误消息中。  
  
 WITH CLEANUP  
 删除无法正常完成的会话一方的所有消息和目录视图条目。 不会向会话的另一方通知此清除操作。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务队列中删除的会话端点、 在传输队列中，会话的所有消息和会话的所有消息。 管理员可以使用此选项删除无法正常完成的会话。 例如，如果某个远程服务已被永久删除，则管理员可以使用 WITH CLEANUP 删除指向该服务的会话。 不要在代码中使用 WITH CLEANUP[!INCLUDE[ssSB](../../includes/sssb-md.md)]应用程序。 如果在接收端点确认收到消息之前运行 END CONVERSATION WITH CLEANUP，则发送端点将再次发送该消息。 这可能导致再次运行该对话。  
  
## <a name="remarks"></a>注释  
 结束会话锁会话组提供*conversation_handle*属于。 当会话结束时，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 将从服务队列中删除该会话的所有消息。  
  
 会话结束后，应用程序不能再发送或接收有关该会话的消息。 会话中的参与双方必须调用 END CONVERSATION 才能完成该会话。 如果 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 未从会话的另一个参与者那里收到结束对话消息或错误消息，则 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 会向会话中的该参与者发出会话已结束的通知。 在这种情况下，尽管会话的会话句柄已经无效，但会话的端点仍保持活动状态，直到承载远程服务的实例确认该消息。  
  
 如果 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 尚未处理会话的结束对话消息或错误消息，则 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 会向远程会话方发出会话已结束通知。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 发送给远程服务的消息取决于指定的选项：  
  
-   如果会话结束且不错误和对话转接到的远程服务是否仍处于活动状态，[!INCLUDE[ssSB](../../includes/sssb-md.md)]发送类型的消息的`http://schemas.microsoft.com/SQL/ServiceBroker/EndDialog`向远程服务。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 按会话顺序将此消息添加到传输队列中。 在发送此消息之前，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 将发送该会话当前在传输队列中的所有消息。  
  
-   如果以错误结束会话，并且向远程服务会话仍处于活动状态，[!INCLUDE[ssSB](../../includes/sssb-md.md)]发送类型的消息的`http://schemas.microsoft.com/SQL/ServiceBroker/Error`向远程服务。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将删除该会话当前在传输队列中的任何其他消息。  
  
-   使用 WITH CLEANUP 子句，数据库管理员可以删除无法正常完成的会话。 此选项会删除会话中的所有消息和目录视图条目。 请注意，在这种情况下，远程会话方不会收到会话已结束的指示，而且也可能收不到应用程序已发送但尚未通过网络传输的消息。 除非会话不能正常完成，否则请避免使用此选项。  
  
 会话结束后，指定了会话句柄的 [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND 语句将导致 [!INCLUDE[tsql](../../includes/tsql-md.md)] 错误。 如果会话消息发送自会话的另一方，则 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将放弃这些消息。  
  
 如果会话已结束，而远程服务仍未发送会话消息，则远程服务将删除这些未发送的消息。 这不会被视为一个错误，而且远程服务不会收到消息已被删除的通知。  
  
 在 WITH ERROR 子句中指定的失败代码必须是正数。 负数被保留以用于 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 错误消息。  
  
 END CONVERSATION 在用户定义函数中无效。  
  
## <a name="permissions"></a>Permissions  
 若要结束活动会话，当前用户必须为会话的所有者、sysadmin 固定服务器角色的成员或 db_owner 固定数据库角色的成员。  
  
 sysadmin 固定服务器角色的成员或 db_owner 固定数据库角色的成员可以使用 WITH CLEANUP 删除已经完成的会话的元数据。  
  
## <a name="examples"></a>示例  
  
### <a name="a-ending-a-conversation"></a>A. 结束会话  
 下例将结束由 `@dialog_handle` 指定的对话。  
  
```  
END CONVERSATION @dialog_handle ;  
```  
  
### <a name="b-ending-a-conversation-with-an-error"></a>B. 结束发生错误的会话  
 下例将在处理语句报告错误时，结束由 `@dialog_handle` 指定的对话并返回错误。 请注意，这是一个简单的错误处理方法，可能不适用于某些应用程序。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ErrorSave INT,  
        @ErrorDesc NVARCHAR(100) ;  
BEGIN TRANSACTION ;  
  
<receive and process message>  
  
SET @ErrorSave = @@ERROR ;  
  
IF (@ErrorSave <> 0)  
  BEGIN  
      ROLLBACK TRANSACTION ;  
      SET @ErrorDesc = N'An error has occurred.' ;  
      END CONVERSATION @dialog_handle   
      WITH ERROR = @ErrorSave DESCRIPTION = @ErrorDesc ;  
  END  
ELSE  
  
COMMIT TRANSACTION ;  
```  
  
### <a name="c-cleaning-up-a-conversation-that-cannot-complete-normally"></a>C. 清理无法正常完成的会话  
 下例将结束由 `@dialog_handle` 指定的对话。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将立即从服务队列和传输队列中删除所有消息而不通知远程服务。 由于结束与清理进行对话，则不通知远程服务，应仅使用此参数不能接收远程服务的情况下**EndDialog**或**错误**消息。  
  
```  
END CONVERSATION @dialog_handle WITH CLEANUP ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [开始会话定时器 &#40;Transact SQL &#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [BEGIN DIALOG CONVERSATION &#40;Transact SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  

