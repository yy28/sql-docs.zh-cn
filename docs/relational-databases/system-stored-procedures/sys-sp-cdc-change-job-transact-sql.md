---
title: sys. sp_cdc_change_job （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
author: rothja
ms.author: jroth
ms.openlocfilehash: 4bd906f9a359a73a15d89a4cb60b6646a2abe53a
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305062"
---
# <a name="syssp_cdc_change_job-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改当前数据库中变更数据捕获清除或捕获作业的配置。 若要查看作业的当前配置，请查询 " [_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) " 表，或使用 " [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)"。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_change_job [ [ @job_type = ] 'job_type' ]  
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ @threshold = ] 'delete threshold'  
```  
  
## <a name="arguments"></a>参数  
要修改的作业 @no__t 0 类型。 *job_type*的值为**nvarchar （20）** ，默认值为 "捕获"。 有效的输入为 'capture' 和 'cleanup'。  
  
要在每个扫描周期中处理的最大事务数 @no__t 0。 *max_trans*的默认值为**int** ，默认值为 NULL，表示未更改此参数。 如果指定值，则该值必须是一个正整数。  
  
 *max_trans*仅对捕获作业有效。  
  
@no__t 为从日志中提取所有行而要执行的扫描周期的最大数目。 *max_scans*的默认值为**int** ，默认值为 NULL，表示未更改此参数。  
  
 *max_scan*仅对捕获作业有效。  
  
`[ @continuous ] = continuous_` 指示捕获作业是要连续运行（1）还是仅运行一次（0）。 *连续*为**bit** ，默认值为 NULL，指示未更改此参数。  
  
 当*连续*= 1 时， [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)作业将扫描日志，并处理最多（*max_trans* @no__t 3 *max_scans*）的事务。 然后，在开始下一次日志扫描之前，会等待*polling_interval*中指定的秒数。  
  
 当*连续*= 0 时， **sp_cdc_scan**作业最多执行日志的*max_scans*扫描，每次扫描时最多处理*max_trans*事务，然后退出。  
  
 如果 **@no__t 1continuous**从1更改为0， **\@pollinginterval**将自动设置为0。 将忽略为 **\@pollinginterval**以外的值指定的值。  
  
 如果省略 **@no__t 1continuous**或将其显式设置为 NULL，并且 **\@pollinginterval**显式设置为大于0的值，则 **\@continuous**自动设置为1。  
  
 *连续*仅对捕获作业有效。  
  
@no__t-每个日志扫描周期的秒数为0。 *polling_interval*的默认值为**bigint** ，默认值为 NULL，指示未更改此参数。  
  
 当*连续*设置为1时， *polling_interval*仅对捕获作业有效。  
  
@no__t-在更改表中保留更改行的分钟数。 *保留期*为**bigint** ，默认值为 NULL，指示未更改此参数。 最大值为 52494800（100 年）。 如果指定值，则该值必须是一个正整数。  
  
 *保留*仅对清除作业有效。  
  
@no__t 在清除时使用单个语句可以删除的删除项的最大数目为0。 *delete 阈值*为**bigint** ，默认值为 NULL，指示未更改此参数。 *delete 阈值*仅对清除作业有效。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 如果省略参数，则不会更新[_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)表中的关联值。 如果将参数显式设置为 NULL，则视作省略此参数。  
  
 如果指定的参数对相应作业类型无效，则会导致该语句失败。  
  
 直到使用[sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)停止作业并使用[sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)重新启动作业后，对作业的更改才会生效。  
  
## <a name="permissions"></a>权限  
 要求具有**db_owner**固定数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-a-capture-job"></a>A. 更改捕获作业  
 下面的示例在 @no__t 3 数据库中更新捕获作业的 `@job_type`、`@maxscans` 和 @no__t 2 参数。 省略了捕获作业的其他有效参数（`@continuous` 和 `@pollinginterval`）；未修改它们的值。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>B. 更改清除作业  
 下例更新 `AdventureWorks2012` 数据库中的一个清除作业。 为此作业类型（ **@threshold** 除外）的所有有效参数均已指定。 不修改 **@no__t 值-1**的值。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [dbo.cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
