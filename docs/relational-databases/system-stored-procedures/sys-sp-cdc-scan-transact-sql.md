---
title: sys.sp_cdc_scan (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b143e1ee7642774ae08ddd685a6c3fc6b641180f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysspcdcscan-transact-sql"></a>sys.sp_cdc_scan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  执行变更数据捕获日志扫描操作。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@maxtrans=** ] *max_trans*  
 每个扫描循环中要处理的最大事务数。 *max_trans*是**int**默认值为 500。  
  
 [  **@maxscans=** ] *max_scans*  
 为了从日志中提取所有行而要执行的最大扫描循环次数。 *max_scans*是**int**默认值为 10。  
  
 [  **@continuous=** ]*连续*  
 指示存储的过程是否应执行单个扫描循环 (0) 后结束，或连续运行，为指定的时间暂停*polling_interval*之前 reexecuting 扫描周期 (1)。 *连续*是**tinyint**默认值为 0。  
  
 [  **@pollinginterval=** ] *polling_interval*  
 日志扫描周期之间的秒数。 *polling_interval*是**bigint**默认值为 0。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 如果变更数据捕获正在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理捕获作业，则 sys.sp_MScdc_capture_job 将内部调用 sys.sp_cdc_scan。 如果变更数据捕获日志扫描操作已经处于活动状态，或数据库启用了事务复制，则无法显式执行此过程。 此存储过程应当由需要自定义自动配置的捕获作业的行为的管理员使用。  
  
## <a name="permissions"></a>权限  
 要求具有 db_owner 固定数据库角色中的成员资格。  
  
## <a name="see-also"></a>另请参阅  
 [dbo.cdc_jobs &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
