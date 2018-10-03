---
title: sp_delete_alert (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_alert_TSQL
- sp_delete_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_alert
ms.assetid: a831315e-793d-41c4-8333-b324bb2bc614
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e912c8d849ec30554e4213979e626d1710f9a9df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718925"
---
# <a name="spdeletealert-transact-sql"></a>sp_delete_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除警报。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_alert [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>参数  
 [ **@name=** ] **'***name***'**  
 警报的名称。 *名称*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 删除警报时，将同时删除与警报相关的所有通知。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色才能执行此过程。  
  
## <a name="examples"></a>示例  
 以下示例将删除一个名为 `Test Alert` 的警报。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_alert  
   @name = N'Test Alert' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_add_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
