---
title: sp_add_category (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 295f29b86e53a8d58622e4c79c1b36734acdbe3e
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591011"
---
# <a name="spaddcategory-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将指定的作业、警报或操作员类别添加到服务器中。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>参数  
 [  **@class =** ] **'**_类_  
 要添加的类别的类。 *类*是**varchar(8)** 的作业，默认值可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|JOB|添加作业类别。|  
|ALERT|添加警报类别。|  
|OPERATOR|添加操作员类别。|  
  
 [  **@type =** ] **'**_类型_  
 要添加的类别的类型。 *类型*是**varchar(12)**，默认值为**本地**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|LOCAL|本地作业类别。|  
|多服务器|多服务器作业类别。|  
|无|非 JOB 类类别 **。**|  
  
 [  **@name =** ] **'**_名称_  
 要添加的类别的名称。 该名称在指定类中必须是唯一的。 *名称*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_add_category**必须从运行**msdb**数据库。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_add_category**。  
  
## <a name="examples"></a>示例  
 以下示例将创建一个名为 `AdminJobs` 的本地作业类别。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_delete_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [dbo.sysjobs &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
