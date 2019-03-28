---
title: sp_post_msx_operation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f36ad40a2b16401218fe2a5927407464fe6ac11b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536120"
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将操作 （行） 插入到**sysdownloadlist**的目标服务器可以下载并执行的系统表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_post_msx_operation  
     [ @operation = ] 'operation'  
     [ , [ @object_type = ] 'object' ]   
     { , [ @job_id = ] job_id }   
     [ , [ @specific_target_server = ] 'target_server' ]   
     [ , [ @value = ] value ]  
     [ , [ @schedule_uid = ] schedule_uid ]  
```  
  
## <a name="arguments"></a>参数  
`[ @operation = ] 'operation'` 已发布操作的操作的类型。 *操作*是**varchar(64)**，无默认值。 有效的操作取决于*object_type*。  
  
|对象类型|操作|  
|-----------------|---------------|  
|**JOB**|Insert<br /><br /> UPDATE<br /><br /> DELETE<br /><br /> START<br /><br /> STOP|  
|**SERVER**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**计划**|Insert<br /><br /> UPDATE<br /><br /> DELETE|  
  
`[ @object_type = ] 'object'` 要为其发布操作的对象的类型。 有效类型为**作业**，**服务器**，并**计划**。 *对象*是**varchar(64)**，默认值为**作业**。  
  
`[ @job_id = ] job_id` 应用操作的作业作业标识号。 *job_id*是**uniqueidentifier**，无默认值。 **0x00**表示所有作业。 如果*对象*是**服务器**，然后*job_id*不是必需的。  
  
`[ @specific_target_server = ] 'target_server'` 应用指定的操作的目标服务器的名称。 如果*job_id*指定，但*target_server*未指定，则该作业的所有作业服务器发布操作。 *target_server*是**nvarchar(30)**，默认值为 NULL。  
  
`[ @value = ] value` 轮询间隔，以秒为单位。 *value* 的数据类型为 **int**，默认值为 NULL。 指定此参数仅当*操作*是**SET-POLL**。  
  
`[ @schedule_uid = ] schedule_uid` 应用操作计划的唯一标识符。 *schedule_uid*是**uniqueidentifier**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_post_msx_operation**必须从运行**msdb**数据库。  
  
 **sp_post_msx_operation**可以始终安全地调用因为它首先确定如果当前服务器是多服务器的 Microsoft SQL Server 代理，如果是，是否*对象*是一个多服务器作业。  
  
 已发布操作后，它将出现在**sysdownloadlist**表。 创建并发布作业后，对该作业的后续更改也必须通知目标服务器 (TSX)。 这也是用下载列表完成的。  
  
 我们强烈建议使用 SQL Server Management Studio 来管理下载列表。 有关详细信息，请参阅[查看或修改作业](../../ssms/agent/view-or-modify-jobs.md)。  
  
## <a name="permissions"></a>权限  
 若要运行此存储的过程，必须授予用户**sysadmin**固定的服务器角色。  
  
## <a name="see-also"></a>请参阅  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
