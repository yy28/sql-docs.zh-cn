---
title: "创建协定 (Transact SQL) |Microsoft 文档"
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
- CONTRACT_TSQL
- CREATE_CONTRACT_TSQL
- CREATE CONTRACT
- CONTRACT
dev_langs: TSQL
helpviewer_keywords:
- CREATE CONTRACT statement
- contracts [Service Broker], creating
- message types [Service Broker], contracts
ms.assetid: 494cbfa6-8e93-4161-a64d-90d681915211
caps.latest.revision: "48"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b77fba7800b8533793f9b26574d442bb0c087b8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-contract-transact-sql"></a>CREATE CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建新约定。 约定用于定义在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 会话中所使用的消息类型，还用于确定会话的哪一端可以发送该类型的消息。 每个会话都要遵循一个约定。 当会话开始时，启动服务为会话指定约定。 目标服务指定该目标服务将接受其会话的约定。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE CONTRACT contract_name  
   [ AUTHORIZATION owner_name ]  
      (  {   { message_type_name | [ DEFAULT ] }  
          SENT BY { INITIATOR | TARGET | ANY }   
       } [ ,...n] )   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *contract_name*  
 要创建的约定的名称。 新约定创建于当前数据库中，并且由 AUTHORIZATION 子句中所指定的主体拥有。 不能指定服务器、数据库和架构名称。 *Contract_name*可达 128 个字符。  
  
> [!NOTE]  
>  不要创建使用该关键字的协定的任何*contract_name*。 在 CREATE BROKER PRIORITY 中为约定名称指定 ANY 时，优先级将被视为针对所有约定。 此情况不限于名称为 ANY 的约定。  
  
 授权*owner_name*  
 将约定的所有者设置为指定的数据库用户或角色。 当前用户的工作时**dbo**或**sa**， *owner_name*可以是任何有效的用户或角色的名称。 否则为*owner_name*必须是当前用户的名称、 当前用户具有模拟权限的用户的名称或当前用户所属角色的名称。 如果省略此子句，则约定属于当前用户。  
  
 *message_type_name*  
 要作为约定的一部分所包括的消息类型的名称。  
  
 SENT BY  
 指定哪个端点可以发送所指示的消息类型的消息。 约定将记录服务可以用来拥有特定会话的消息。 每个会话具有两个终结点：*发起程序*终结点、 开始了会话，该服务与*目标*终结点、 联系发起方服务。  
  
 INITIATOR  
 指示只有会话的发起方才能发送指定消息类型的消息。 启动会话的服务称为*发起程序*的会话。  
  
 TARGET  
 指示只有会话的目标才能发送指定消息类型的消息。 接受已由另一个服务启动的会话的服务称为*目标*的会话。  
  
 ANY  
 指示发起方和目标都可以发送此类型的消息。  
  
 [ DEFAULT ]  
 指示此约定支持默认消息类型的消息。 默认情况下，所有数据库都包含名为 DEFAULT 的消息类型。 此消息类型使用的验证为 NONE。 在此子句的上下文中，DEFAULT 不是关键字，必须作为标识符进行分隔。 Microsoft SQL Server 还提供了 DEFAULT 约定，该约定指定 DEFAULT 消息类型。  
  
## <a name="remarks"></a>注释  
 在约定中消息类型的顺序并不重要。 目标收到第一条消息之后，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 允许会话的任一端在任何时候发送允许该会话端发送的任何消息。 例如，如果会话的发起方可以发送的消息类型**//Adventure-Works.com/Expenses/SubmitExpense**，[!INCLUDE[ssSB](../../includes/sssb-md.md)]允许发起方发送任何数量的**SubmitExpense**会话期间的消息。  
  
 无法更改约定中的消息类型和方向。 若要更改约定的 AUTHORIZATION，请使用 ALTER AUTHORIZATION 语句。  
  
 约定必须允许发起方发送消息。 如果约定未包含至少一个 SENT BY ANY 或 SENT BY INITIATOR 消息类型，CREATE CONTRACT 语句将失败。  
  
 而不管协定，一种服务始终可以接收的消息类型`http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`， `http://schemas.microsoft.com/SQL/ServiceBroker/Error`，和`http://schemas.microsoft.com/SQL/ServiceBroker/EndDialog`。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将这些消息类型用于发送到应用程序的系统消息。  
  
 约定不能是临时对象。 约定名称允许以 # 开头，但应当是永久对象。  
  
## <a name="permissions"></a>Permissions  
 默认情况下，成员的**db_ddladmin**或**db_owner**固定数据库角色的成员和**sysadmin**固定的服务器角色可以创建协定。  
  
 默认情况下，协定的成员的所有者**db_ddladmin**或**db_owner**固定数据库角色和成员的**sysadmin**固定的服务器角色具有引用在协定上的权限。  
  
 执行 CREATE CONTRACT 语句的用户必须对所指定的所有消息类型拥有 REFERENCES 权限。  
  
## <a name="examples"></a>示例  
 **A.创建协定**  
  
 以下示例基于三个消息类型创建费用归还约定。  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE           
    [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
    VALIDATION= WELL_FORMED_XML ;           
  
CREATE CONTRACT            
    [//Adventure-Works.com/Expenses/ExpenseSubmission]           
    ( [//Adventure-Works.com/Expenses/SubmitExpense]           
          SENT BY INITIATOR,           
      [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
          SENT BY TARGET,           
      [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
          SENT BY TARGET           
    ) ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [删除协定 &#40;Transact SQL &#41;](../../t-sql/statements/drop-contract-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
