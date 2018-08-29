---
title: sys.sp_cdc_start_job (TRANSACT-SQL) |Microsoft Docs
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
- sp_cdc_start_job
- sp_cdc_start_job_TSQL
- sys.sp_cdc_start_job_TSQL
- sys.sp_cdc_start_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_start_job
ms.assetid: cf443a67-7705-4799-9f39-0e3a6a8a0708
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0e744a907cf7991c0e913bc8a240a5743b91d8a2
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031545"
---
# <a name="sysspcdcstartjob-transact-sql"></a>sys.sp_cdc_start_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  启动当前数据库的变更数据捕获清除或捕获作业。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_start_job [ [ @job_type = ] 'job_type' ]  
```  
  
## <a name="arguments"></a>参数  
 [[  **@job_type=** ] **'***job_type***** ]  
 要添加的作业类型。 *job_type*是**nvarchar(20)** 默认值为**捕获**。 有效输入包括**捕获**并**清理**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>Remarks  
 管理员可以使用 sys.sp_cdc_start_job 显式启动捕获作业或清除作业。  
  
## <a name="permissions"></a>Permissions  
 要求具有 db_owner 固定数据库角色中的成员资格。  
  
## <a name="examples"></a>示例  
  
### <a name="a-starting-a-capture-job"></a>A. 启动捕获作业  
 下面的示例启动 `AdventureWorks2012` 数据库的捕获作业。 为指定值*job_type*不需要，因为默认作业类型为**捕获**。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_start_job;  
GO  
```  
  
### <a name="b-starting-a-cleanup-job"></a>B. 启动清除作业  
 下例启动 `AdventureWorks2012` 数据库的一个清除作业。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_start_job @job_type = N'cleanup';  
```  
  
## <a name="see-also"></a>请参阅  
 [dbo.cdc_jobs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_stop_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)  
  
  
