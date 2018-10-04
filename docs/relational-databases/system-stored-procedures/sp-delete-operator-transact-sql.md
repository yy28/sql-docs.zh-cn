---
title: sp_delete_operator (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_operator
- sp_delete_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_operator
ms.assetid: ff6c2c4b-e9fe-4d0c-bbc2-a2ddcc1acb95
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2b55d44a837cc721761ebe77352962d1dea88f55
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704655"
---
# <a name="spdeleteoperator-transact-sql"></a>sp_delete_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除一位操作员。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_operator [ @name = ] 'name'   
     [ , [ @reassign_to_operator = ] 'reassign_operator' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@name=** ] **'***name***'**  
 要删除的操作员的名称。 *名称*是**sysname**，无默认值。  
  
 [ **@reassign_to_operator=** ]  **'***reassign_operator***'**  
 操作员的名称，指定操作员的警报将重新分配给此操作员。 *reassign_operator*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 删除操作员时，将同时删除与此操作员关联的所有通知。  
  
## <a name="permissions"></a>Permissions  
 成员**sysadmin**固定的服务器角色可以执行**sp_delete_operator**。  
  
## <a name="examples"></a>示例  
 以下示例将删除操作员 `François Ajenstat`。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_operator @name = 'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_add_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
