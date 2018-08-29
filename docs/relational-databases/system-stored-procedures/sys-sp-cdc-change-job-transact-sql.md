---
title: sys.sp_cdc_change_job (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7603f20095fa09bfcd574aeea1bcad5ca357cd40
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43018063"
---
# <a name="sysspcdcchangejob-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改当前数据库中变更数据捕获清除或捕获作业的配置。 若要查看作业的当前配置，请查询[dbo.cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)表，或者使用[sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)。  
  
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
 [  **@job_type=** ] **'***job_type*****  
 要修改的作业类型。 *job_type*是**nvarchar(20)** 默认值为 'capture'。 有效的输入为 'capture' 和 'cleanup'。  
  
 [ **@maxtrans** ] **= * * * max_trans*  
 每个扫描循环中要处理的最大事务数。 *max_trans*是**int** ，默认值为 NULL，指示未更改此参数。 如果指定值，则该值必须是一个正整数。  
  
 *max_trans*仅对捕获作业有效。  
  
 [ **@maxscans** ] **= * * * max_scans*  
 为了从日志中提取所有行而要执行的最大扫描循环次数。 *max_scans*是**int** ，默认值为 NULL，指示未更改此参数。  
  
 *max_scan*仅对捕获作业有效。  
  
 [ **@continuous** ] **= * * * 连续*  
 指示捕获作业是要连续运行 (1) 还是仅运行一次 (0)。 *持续*是**位**，默认值为 NULL，指示未更改此参数。  
  
 当*连续*= 1， [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)作业将扫描日志并且最多可处理 (*max_trans* \* *max_scans*)事务。 然后，在等待中指定的秒数*polling_interval*开始下一次日志扫描之前。  
  
 当*连续*= 0， **sp_cdc_scan**最多执行作业*max_scans*扫描日志，最多处理*max_trans*事务在每个扫描以及然后退出。  
  
 如果**@continuous**从 1 更改为 0， **@pollinginterval**自动设置为 0。 为指定的值**@pollinginterval**而不将忽略 0。  
  
 如果**@continuous**忽略或显式设置为 NULL 并且**@pollinginterval**显式设置为值大于 0， **@continuous**自动设置为 1。  
  
 *连续*仅对捕获作业有效。  
  
 [ **@pollinginterval** ] **= * * * polling_interval*  
 日志扫描循环之间相隔的秒数。 *polling_interval*是**bigint** ，默认值为 NULL，指示未更改此参数。  
  
 *polling_interval*仅对捕获的有效作业*连续*设置为 1。  
  
 [ **@retention** ] **= * * * 保留期*  
 要更改表中保留更改行的分钟数。 *保留期*是**bigint** ，默认值为 NULL，指示未更改此参数。 最大值为 52494800（100 年）。 如果指定值，则该值必须是一个正整数。  
  
 *保留期*仅对清除作业有效。  
  
 [  **@threshold=** ] **'***删除阈值*****  
 可以使用一条语句上清理已删除的删除项的最大数目。 *删除阈值*是**bigint** ，默认值为 NULL，指示未更改此参数。 *删除阈值*仅对清除作业有效。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>Remarks  
 如果省略一个参数，则在关联的值[dbo.cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)表不会更新。 如果将参数显式设置为 NULL，则视作省略此参数。  
  
 如果指定的参数对相应作业类型无效，则会导致该语句失败。  
  
 直到显示作业已停止使用到作业的更改不会生效[sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)并使用重新启动[sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**db_owner**固定的数据库角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-a-capture-job"></a>A. 更改捕获作业  
 以下示例更新`@job_type`， `@maxscans`，并`@maxtrans`参数中的捕获作业`AdventureWorks2012`数据库。 省略了捕获作业的其他有效参数（`@continuous` 和 `@pollinginterval`）；未修改它们的值。  
  
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
 下例更新 `AdventureWorks2012` 数据库中的一个清除作业。 所有有效参数为此作业类型时，除**@threshold**，指定。 值**@threshold**则不会修改。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [dbo.cdc_jobs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
