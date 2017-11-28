---
title: "移动对话 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
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
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs: TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7367254b7dad104c7503c33777d26316a542b4ca
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将会话移动到不同的会话组。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *conversation_handle*  
 一个变量或常量，包含要移动的会话的会话句柄。 *conversation_handle*的类型必须为**uniqueidentifier**。  
  
 到*conversation_group_id*  
 一个变量或常量，包含会话将要移至的会话组的标识符。 *conversation_group_id*的类型必须为**uniqueidentifier**。  
  
## <a name="remarks"></a>注释  
 移动 CONVERSATION 语句移动指定的会话*conversation_handle*到由标识的会话组*conversation_group_id*。 只能在与相同队列关联的会话组之间重定向对话框。  
  
> [!IMPORTANT]  
>  如果移动对话语句不是在批处理或存储的过程的第一个语句，必须以分号结尾前面的语句 (**;**)，则[!INCLUDE[tsql](../../includes/tsql-md.md)]语句终止符。  
  
 移动 CONVERSATION 语句锁定与关联的会话组*conversation_handle*和按指定的会话组*conversation_group_id*直到事务包含该语句提交或回滚。  
  
 MOVE CONVERSATION 在用户定义函数中无效。  
  
## <a name="permissions"></a>Permissions  
 若要移动会话，当前用户必须是会话和会话组的所有者，或者是 sysadmin 固定服务器角色的成员或 db_owner 固定数据库角色的成员。  
  
## <a name="examples"></a>示例  
 下面的示例将会话移动到不同的会话组。  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER,  
        @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_handle =  
    <retrieve conversation handle from database> ;  
SET @conversation_group_id =  
    <retrieve conversation group ID from database> ;  
  
MOVE CONVERSATION @conversation_handle TO @conversation_group_id ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN DIALOG CONVERSATION &#40;Transact SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;Transact SQL &#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40;Transact SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
