---
title: "发送 (Transact SQL) |Microsoft 文档"
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
- SEND_ON_CONVERSATION_TSQL
- ON_CONVERSATION_TSQL
- SEND
- SEND_TSQL
- SEND ON CONVERSATION
- ON CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], message sending
- SEND statement
- messages [Service Broker], sending
- sending messages
ms.assetid: b6e66aeb-1714-4c2b-b7c2-d386d77b0d46
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b149c44df4fb417ed143147cd38b4ae838318ece
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="send-transact-sql"></a>SEND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用一个或多个现有会话发送消息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SEND  
   ON CONVERSATION [(]conversation_handle [,.. @conversation_handle_n][)]  
   [ MESSAGE TYPE message_type_name ]  
   [ ( message_body_expression ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 会话*conversation_handle [...@conversation_handle_n]*  
 指定消息所属的对话。 *Conversation_handle*必须包含有效的会话标识符。 不能多次使用相同的会话句柄。  
  
 消息类型*message_type_name*  
 指定发送的消息的消息类型。 必须将此消息类型包含在这些会话使用的服务约定中。 这些约定必须允许从此会话方发送该类型的消息。 例如，会话的目标服务只能发送在约定中指定为 SENT BY TARGET 或 SENT BY ANY 的消息。 如果省略此子句，则消息类型为 DEFAULT。  
  
 *message_body_expression*  
 提供一个表示消息主体的表达式。 *Message_body_expression*是可选的。 但是，如果*message_body_expression*存在的表达式必须是可以转换为的类型**varbinary （max)**。 该表达式不能为 NULL。 如果省略该子句，则消息主体为空。  
  
## <a name="remarks"></a>注释  
  
> [!IMPORTANT]  
>  如果 SEND 语句不是批处理或存储过程中的第一个语句，则必须使用分号 (;) 终止其前面的语句。  
  
 SEND 语句将来自一个或多个 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 会话一端的服务的消息传送到这些会话另一端的服务。 然后，使用 RECEIVE 语句从目标服务的关联队列中检索发送的消息。  
  
 提供给 ON CONVERSATION 子句的会话句柄来自以下三个来源之一：  
  
-   如果发送的消息不是为了响应从另一服务收到的消息，则使用从创建此会话的 BEGIN DIALOG 语句返回的会话句柄。  
  
-   如果发送的消息是为了响应之前从另一服务收到的消息，则使用由返回原始消息的 RECEIVE 语句返回的会话句柄。  
  
 在许多情况下包含发送语句的代码是独立于包含提供会话句柄的 BEGIN DIALOG 或 RECEIVE 语句的代码。 在这些情况下，会话句柄必须是传递给包含 SEND 语句的代码的状态信息中的数据项之一。  
  
 发送到其他 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例中的服务的消息将存储在当前数据库的传输队列中，直到可以将这些消息传输到远程实例中的服务队列为止。 发送到同一[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例中的服务的消息被直接放入与这些服务关联的队列中。 如果因出现某种情况导致无法将本地消息直接放入目标服务队列中，则可以先将本地消息存储在传输队列中，直到解决了这种情况为止。 发生某些类型的错误或目标服务队列处于非活动状态就是出现这种情况的例子。 你可以使用**sys.transmission_queue**系统视图以查看传输队列中的消息。  
  
 SEND 是一个原子语句，即，如果在多个会话中发送消息的 SEND 语句失败（例如，由于对话处于错误状态），则不会将任何消息存储在传输队列中，也不会将消息放入任何目标服务队列中。  
  
 Service Broker 优化使用相同 SEND 语句在多个会话中发送的消息的存储和传输。  
  
 一个实例的传输队列中的消息按照以下顺序传输：  
  
-   与其关联的会话端点的优先级别。  
  
-   在优先级别内，依照它们在会话中的发送顺序。  
  
 如果 HONOR_BROKER_PRIORITY 数据库选项设置为 ON，则会话优先级中指定的优先级别仅应用于传输队列中的消息。 如果 HONOR_BROKER_PRIORITY 设置为 OFF，则会为放入该数据库的传输队列中的所有消息都分配默认优先级别 5。 优先级别不适用于将消息直接放入同一[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的服务队列中的 SEND。  
  
 SEND 语句分别锁定发送消息的每个会话，以确保每个会话按顺序传送消息。  
  
 SEND 在用户定义的函数中无效。  
  
## <a name="permissions"></a>Permissions  
 若要发送消息，当前用户必须在每个发送消息的服务的队列中具有 RECEIVE 权限。  
  
## <a name="examples"></a>示例  
 以下示例启动一个对话，并在该对话中发送一条 XML 消息。 若要发送消息，该示例 xml 将对象转换为**varbinary （max)**。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ExpenseReport XML ;  
  
SET @ExpenseReport = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle  
FROM SERVICE [//Adventure-Works.com/Expenses/ExpenseClient]  
TO SERVICE '//Adventure-Works.com/Expenses'  
ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing] ;  
  
SEND ON CONVERSATION @dialog_handle  
    MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense]  
    (@ExpenseReport) ;  
```  
  
 以下示例启动三个对话，并在每个对话中发送一条 XML 消息。  
  
```  
DECLARE @dialog_handle1 UNIQUEIDENTIFIER,  
        @dialog_handle2 UNIQUEIDENTIFIER,  
        @dialog_handle3 UNIQUEIDENTIFIER,  
        @OrderMsg XML ;  
  
SET @OrderMsg = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle1  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB1/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle2  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB2/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle3  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB3/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
SEND ON CONVERSATION (@dialog_handle1, @dialog_handle2, @dialog_handle3)  
    MESSAGE TYPE [//AllDBs/OrderMsg]  
    (@OrderMsg) ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN DIALOG CONVERSATION &#40;Transact SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;Transact SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [接收 &#40;Transact SQL &#41;](../../t-sql/statements/receive-transact-sql.md)   
 [sys.transmission_queue &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  

