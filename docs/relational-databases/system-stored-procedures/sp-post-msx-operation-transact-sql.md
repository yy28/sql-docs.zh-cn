---
title: sp_post_msx_operation (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f6d0dfc8c9a9925f7bf2fa84c4b9330b99c60c3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261033"
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  插入操作 （行） **sysdownloadlist**目标服务器，可以下载并执行的系统表。  
  
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
 [  **@operation =**] *****操作*****  
 已发布操作的操作类型。 *操作*是**varchar(64)**，无默认值。 有效的操作取决于*object_type*。  
  
|对象类型|运算|  
|-----------------|---------------|  
|**JOB**|Insert<br /><br /> UPDATE<br /><br /> DELETE<br /><br /> START<br /><br /> STOP|  
|**服务器**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**计划**|Insert<br /><br /> UPDATE<br /><br /> DELETE|  
  
 [ **@object_type =**] **'***object***'**  
 将为其发布操作的对象的类型。 有效类型是**作业**，**服务器**，和**计划**。 *对象*是**varchar(64)**，默认值为**作业**。  
  
 [ **@job_id =**] *job_id*  
 应用操作的作业的作业标识号。 *job_id*是**uniqueidentifier**，无默认值。 **0x00**指示所有作业。 如果*对象*是**服务器**，然后*job_id*不是必需的。  
  
 [ **@specific_target_server =**] **'***target_server***'**  
 应用指定操作的目标服务器的名称。 如果*job_id*指定，但*target_server*未指定，则发布操作的所有作业的作业的服务器。 *target_server*是**nvarchar (30)**，默认值为 NULL。  
  
 [ **@value =**] *value*  
 以秒为单位的轮询间隔。 *value* 的数据类型为 **int**，默认值为 NULL。 指定此参数才*操作*是**集轮询**。  
  
 [ **@schedule_uid=** ] *schedule_uid*  
 应用操作的计划的唯一标识符。 *schedule_uid*是**uniqueidentifier**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **sp_post_msx_operation**必须从运行**msdb**数据库。  
  
 **sp_post_msx_operation**可以始终调用，安全地因为会首先确定当前的服务器是否多服务器的 Microsoft SQL Server 代理以及如果是这样，是否*对象*是一个多服务器作业。  
  
 已发布操作后，它将出现在**sysdownloadlist**表。 创建并发布作业后，对该作业的后续更改也必须通知目标服务器 (TSX)。 这也是用下载列表完成的。  
  
 我们强烈建议使用 SQL Server Management Studio 来管理下载列表。 有关详细信息，请参阅[视图或修改作业](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)。  
  
## <a name="permissions"></a>权限  
 若要运行此存储的过程，必须授予用户**sysadmin**固定的服务器角色。  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
