---
title: sp_delete_jobserver （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobserver
- sp_delete_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobserver
ms.assetid: 6d63ed32-68cf-4d8f-aa40-05a3826e05b8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4499183a8cf5019fe7a4ce10bdb9ffc83726551a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831194"
---
# <a name="sp_delete_jobserver-transact-sql"></a>sp_delete_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除指定的目标服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_jobserver { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>参数  
`[ @job_id = ] job_id`要从中删除指定目标服务器的作业的标识号。 *job_id*的值为**uniqueidentifier**，默认值为 NULL。  
  
`[ @job_name = ] 'job_name'`要从中删除指定目标服务器的作业的名称。 *job_name*的默认值为**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  必须指定*job_id*或*job_name* ;不能同时指定两者。  
  
`[ @server_name = ] 'server'`要从指定作业中删除的目标服务器的名称。 *服务器*为**nvarchar （30）**，无默认值。 *服务器*可以是 **（LOCAL）** 或远程目标服务器的名称。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>权限  
 若要运行此存储过程，用户必须是**sysadmin**固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
 下面的示例 `SEATTLE2` 从处理作业中删除服务器 `Weekly Sales Backups` 。  
  
> [!NOTE]  
>  此示例假定事先已创建了 `Weekly Sales Backups` 作业。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_help_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
