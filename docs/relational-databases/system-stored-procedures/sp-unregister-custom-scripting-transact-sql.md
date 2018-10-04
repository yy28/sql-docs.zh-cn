---
title: sp_unregister_custom_scripting (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 778019343c6dfd277196644d5956abb2f93c9121
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647345"
---
# <a name="spunregistercustomscripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储的过程删除用户定义的自定义存储的过程或[!INCLUDE[tsql](../../includes/tsql-md.md)]已由执行注册的脚本文件[sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@type** =] **'***类型*****  
 要删除的自定义存储过程或脚本的类型。 *类型*是**varchar(16)**，无默认值，并且可以是以下值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**insert**|复制 INSERT 语句时，执行注册的自定义存储过程或脚本。|  
|**更新**|复制 UPDATE 语句时，执行注册的自定义存储过程或脚本。|  
|**delete**|复制 DELETE 语句时，执行注册的自定义存储过程或脚本。|  
|**custom_script**|在数据定义语言 (DDL) 触发器的结尾执行已注册的自定义存储过程或脚本。|  
  
 [ **@publication** = ] **'***publication***'**  
 要为其删除自定义存储过程或脚本的发布的名称。 *发布*是**sysname**，默认值为 NULL。  
  
 [ **@article** =] **'***文章*****  
 要为其删除自定义存储过程或脚本的项目的名称。 *文章*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_unregister_custom_scripting**快照和事务复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定服务器角色**db_owner**固定数据库角色或**db_ddladmin**固定的数据库角色可以执行**sp_unregister_custom_scripting**。  
  
## <a name="see-also"></a>请参阅  
 [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
