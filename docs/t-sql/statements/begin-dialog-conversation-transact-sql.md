---
title: "BEGIN DIALOG CONVERSATION (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DIALOG CONVERSATION
- DIALOG
- BEGIN_DIALOG_TSQL
- BEGIN_DIALOG_CONVERSATION_TSQL
- DIALOG_CONVERSATION_TSQL
- DIALOG_TSQL
- BEGIN DIALOG
- BEGIN DIALOG CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker]
- beginning dialogs
- dialogs [Service Broker], beginning
- BEGIN DIALOG CONVERSATION statement
- cryptography [SQL Server], conversations
- opening conversations
- encryption [SQL Server], conversations
- starting conversations
ms.assetid: 8e814f9d-77c1-4906-b8e4-668a86fc94ba
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a2ece31010207b6044504f099c11443a2fec0fa2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="begin-dialog-conversation-transact-sql"></a>BEGIN DIALOG CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  启动从一个服务到另一个服务的对话。 所谓对话，就是让两个服务能够进行一次顺序消息传递。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
BEGIN DIALOG [ CONVERSATION ] @dialog_handle  
   FROM SERVICE initiator_service_name  
   TO SERVICE 'target_service_name'  
       [ , { 'service_broker_guid' | 'CURRENT DATABASE' }]   
   [ ON CONTRACT contract_name ]  
   [ WITH  
   [  { RELATED_CONVERSATION = related_conversation_handle   
      | RELATED_CONVERSATION_GROUP = related_conversation_group_id } ]   
   [ [ , ] LIFETIME = dialog_lifetime ]   
   [ [ , ] ENCRYPTION = { ON | OFF }  ] ]  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 **@***dialog_handle*  
 一个变量，用于为 BEGIN DIALOG CONVERSATION 语句返回的新对话存储系统生成的对话句柄。 变量必须为类型**uniqueidentifier**。  
  
 FROM SERVICE *initiator_service_name*  
 指定启动对话的服务。 指定的名称必须是当前数据库中的服务的名称。 为发起方服务指定的队列将接收由目标服务返回的消息，以及 Service Broker 为此会话创建的消息。  
  
 TO SERVICE **'***target_service_name***'**  
 指定启动对话时的目标服务。 *Target_service_name*属于类型**nvarchar(256)**。 [!INCLUDE[ssSB](../../includes/sssb-md.md)]使用逐字节比较，以匹配*target_service_name*字符串。 换言之，比较时将区分大小写，且不考虑当前的排序规则。  
  
 *service_broker_guid*  
 指定承载目标服务的数据库。 当多个数据库承载目标服务的实例时，你可以通过提供通信与特定数据库*service_broker_guid*。  
  
 *Service_broker_guid*属于类型**nvarchar （128)**。 若要查找*service_broker_guid*对于数据库，在数据库中运行以下查询：  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID() ;  
```  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 当前数据库  
 指定会话使用*service_broker_guid*当前数据库。  
  
 ON CONTRACT *contract_name*  
 指定此会话遵循的约定。 当前数据库中必须有该约定。 如果目标服务不接受遵循指定约定的新会话，则 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将返回针对该会话的错误消息。 当省略此子句时，对话所遵循的名为的协定**默认**。  
  
 RELATED_CONVERSATION **=***related_conversation_handle*  
 指定将新对话添加到的现有会话组。 新建对话框时存在此子句，则属于与对话框中指定相同的会话组*related_conversation_handle*。 *Related_conversation_handle*必须是隐式转换的类型键入**uniqueidentifier**。 如果语句将失败*related_conversation_handle*不引用现有的对话框。  
  
 RELATED_CONVERSATION_GROUP **=***related_conversation_group_id*  
 指定将新对话添加到的现有会话组。 新建对话框时存在此子句，则将添加到指定的会话组*related_conversation_group_id*。 *Related_conversation_group_id*必须是隐式转换的类型键入**uniqueidentifier**。 如果*related_conversation_group_id*不引用现有会话组，service broker 创建新的会话组具有指定*related_conversation_group_id*和与该会话组的新建对话框。  
  
 LIFETIME **=***dialog_lifetime*  
 指定对话将保持打开状态的最长时间。 为使对话成功完成，两个端点都必须在生存期内显式结束对话。 *Dialog_lifetime*值必须以秒为单位。 生存期属于类型**int**。指定没有生存期子句后，对话框生存期将的最大值**int**数据类型。  
  
 ENCRYPTION  
 指定发送之外的实例时是否必须加密此对话框上发送和接收的消息[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 一个对话框，其中必须加密是*安全的对话框*。 如果 ENCRYPTION = ON，但未配置支持加密所需的证书，则 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将返回针对该会话的错误消息。 如果加密 = OFF，如果远程服务绑定配置为使用加密*target_service_name*; 否则发送消息时未加密。 如果未使用此子句，则默认值为 ON。  
  
> [!NOTE]  
>  在任何情况下，都不对同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的服务间交换的消息加密。 但是，如果用于会话的服务位于不同的数据库，则使用加密的会话仍然需要数据库主密钥和加密证书。 这样，在会话进行的过程中，如果将一个数据库移到其他实例，会话仍可继续进行。  
  
## <a name="remarks"></a>注释  
 所有消息都是会话的一部分。 因此，发起方服务必须在发送消息到目标服务之前启动与目标服务的会话。 BEGIN DIALOG CONVERSATION 语句中指定的信息类似于信函上的地址；[!INCLUDE[ssSB](../../includes/sssb-md.md)] 使用此信息将消息传递到正确的服务。 TO SERVICE 子句中指定的服务是消息发送到的地址。 FROM SERVICE 子句中指定的服务是用于答复消息的返回地址。  
  
 会话目标不需要调用 BEGIN DIALOG CONVERSATION。 当会话中来自发起方的第一条消息到达时，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 将在目标数据库中创建一个会话。  
  
 启动一个对话将在发起服务的数据库中创建一个会话端点，但不创建与承载目标服务的实例的网络连接。 在发送第一条消息之前，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 不会建立与对话目标的通信。  
  
 如果 BEGIN DIALOG CONVERSATION 语句未指定相关的会话或相关的会话组，则 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将为新的会话创建一个新的会话组。  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 不允许将会话任意分组。 会话组中的所有会话都必须有 FROM 子句中指定的服务作为会话的发起方或目标。  
  
 BEGIN DIALOG CONVERSATION 命令锁定包含的会话组*dialog_handle*返回。 如果该命令包含 RELATED_CONVERSATION_GROUP 子句的会话组*dialog_handle*中指定的会话组*related_conversation_group_id*参数。 如果该命令包含 RELATED_CONVERSATION 子句的会话组*dialog_handle*与关联的会话组*related_conversation_handle*指定。  
  
 BEGIN DIALOG CONVERSATION 在用户定义函数中无效。  
  
## <a name="permissions"></a>权限  
 若要启动对话，则当前的用户对于在该命令的 FROM 子句中指定的服务的队列必须有 RECEIVE 权限，对于指定的约定有 REFERENCES 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-beginning-a-dialog"></a>A. 启动对话  
 以下实例会启动一个对话会话，并将对话的标识符存储于 `@dialog_handle.`。`//Adventure-Works.com/ExpenseClient` 服务是对话的发起方，`//Adventure-Works.com/Expenses` 服务是对话的目标。 对话遵循约定 `//Adventure-Works.com/Expenses/ExpenseSubmission`。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
### <a name="b-beginning-a-dialog-with-an-explicit-lifetime"></a>B. 启动具有显式生存期的对话  
 以下实例将启动一个对话会话，并将对话的标识符存储于 `@dialog_handle`。 `//Adventure-Works.com/ExpenseClient` 服务是对话的发起方，`//Adventure-Works.com/Expenses` 服务是对话的目标。 对话遵循约定 `//Adventure-Works.com/Expenses/ExpenseSubmission`。 如果 END CONVERSATION 命令在 `60` 秒内未关闭此对话，则 Broker 将结束此对话并返回错误。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH LIFETIME = 60 ;  
```  
  
### <a name="c-beginning-a-dialog-with-a-specific-broker-instance"></a>C. 启动具有特定 Broker 实例的对话  
 以下实例将启动一个对话会话，并将对话的标识符存储于 `@dialog_handle`。 `//Adventure-Works.com/ExpenseClient` 服务是对话的发起方，`//Adventure-Works.com/Expenses` 服务是对话的目标。 对话遵循约定 `//Adventure-Works.com/Expenses/ExpenseSubmission`。 Broker 将此对话的消息路由到由 GUID `a326e034-d4cf-4e8b-8d98-4d7e1926c904.` 标识的 Broker。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses',   
              'a326e034-d4cf-4e8b-8d98-4d7e1926c904'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
### <a name="d-beginning-a-dialog-and-relating-it-to-an-existing-conversation-group"></a>D. 启动一个对话，并将其关联到现有的会话组  
 以下实例将启动一个对话会话，并将对话的标识符存储于 `@dialog_handle`。 `//Adventure-Works.com/ExpenseClient` 服务是对话的发起方，`//Adventure-Works.com/Expenses` 服务是对话的目标。 对话遵循约定 `//Adventure-Works.com/Expenses/ExpenseSubmission`。 Broker 将此对话与由 `@conversation_group_id` 标识的会话组关联，而不创建新的会话组。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_group_id = <retrieve conversation group ID from database>  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH RELATED_CONVERSATION_GROUP = @conversation_group_id ;  
```  
  
### <a name="e-beginning-a-dialog-with-an-explicit-lifetime-and-relating-the-dialog-to-an-existing-conversation"></a>E. 启动一个具有显式生存期的对话，并将其关联到现有会话  
 以下实例将启动一个对话会话，并将对话的标识符存储于 `@dialog_handle`。 `//Adventure-Works.com/ExpenseClient` 服务是对话的发起方，`//Adventure-Works.com/Expenses` 服务是对话的目标。 对话遵循约定 `//Adventure-Works.com/Expenses/ExpenseSubmission`。 新对话与 `@existing_conversation_handle` 属于同一个会话组。 如果 END CONVERSATION 命令在 `600` 秒内未关闭此对话，则 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将结束此对话并返回错误。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER  
DECLARE @existing_conversation_handle UNIQUEIDENTIFIER  
  
SET @existing_conversation_handle = <retrieve conversation handle from database>  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH RELATED_CONVERSATION = @existing_conversation_handle  
   LIFETIME = 600 ;  
```  
  
### <a name="f-beginning-a-dialog-with-optional-encryption"></a>F. 启动具有可选加密的对话  
 以下实例将启动一个对话，并将对话的标识符存储于 `@dialog_handle`。 `//Adventure-Works.com/ExpenseClient` 服务是对话的发起方，`//Adventure-Works.com/Expenses` 服务是对话的目标。 对话遵循约定 `//Adventure-Works.com/Expenses/ExpenseSubmission`。 如果加密不可用，则此示例中的会话允许消息在不加密的状态下通过网络传输。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH ENCRYPTION = OFF ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [开始会话定时器 &#40;Transact SQL &#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [END CONVERSATION &#40;Transact SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [移动对话 &#40;Transact SQL &#41;](../../t-sql/statements/move-conversation-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
