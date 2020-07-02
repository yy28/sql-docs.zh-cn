---
title: sp_delete_category （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_category_TSQL
- sp_delete_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_category
ms.assetid: 63ea7d0d-a567-456e-a778-bee99e21d16c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cea339352a983028c161cef6fec8643955457b55
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750660"
---
# <a name="sp_delete_category-transact-sql"></a>sp_delete_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  从当前服务器中删除指定的作业、警报或操作员类别。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_category [ @class = ] 'class' , [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>自变量  
`[ @class = ] 'class'`类别的类。 *类*为**varchar （8）**，无默认值，并且必须具有下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**任务**|删除作业类别。|  
|**发出**|删除警报类别。|  
|**操作员**|删除操作员类别。|  
  
`[ @name = ] 'name'`要删除的类别的名称。 *名称*为**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 必须从**msdb**数据库运行**sp_delete_category** 。  
  
 如果删除某个类别，则该类别中的所有作业、警报或操作员将重新分类到类的默认类别中。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能运行此过程。  
  
## <a name="examples"></a>示例  
 以下示例将删除名为 `AdminJobs` 的作业类别。  
  
```  
USE msdb ;  
GO   
  
EXEC dbo.sp_delete_category  
    @name = N'AdminJobs',  
    @class = N'JOB' ;  
GO   
```  
  
## <a name="see-also"></a>请参阅  
 [sp_add_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_help_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
