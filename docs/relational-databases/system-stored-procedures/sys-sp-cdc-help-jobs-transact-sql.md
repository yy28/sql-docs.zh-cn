---
title: sys. sp_cdc_help_jobs （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_jobs
- sys.sp_cdc_help_jobs_TSQL
- sp_cdc_help_jobs_TSQL
- sys.sp_cdc_help_jobs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_help_jobs
ms.assetid: 9399b4bc-8293-408f-b3cb-f904e0657fb5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: beca05cca35d0c410f7e9671d011d913c5ac2f22
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814921"
---
# <a name="syssp_cdc_help_jobs-transact-sql"></a>sys.sp_cdc_help_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告关于当前数据库中所有变更数据捕获清除或捕获作业的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_help_jobs  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作业 ID。|  
|**job_type**|**nvarchar （20）**|作业类型。|  
|**maxtrans**|**int**|在每个扫描循环中要处理的最大事务数。<br /><br /> **maxtrans**仅对捕获作业有效。|  
|**maxscans**|**int**|为了从日志中提取所有行而要执行的扫描周期的最大数目。<br /><br /> **maxscans**仅对捕获作业有效。|  
|**持续**|**bit**|指示捕获作业是连续运行 (1) 还是以一次性模式运行 (0) 的标志。 有关详细信息，请参阅[sys.databases&#41;sp_cdc_add_job &#40;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)。<br /><br /> **连续**仅对捕获作业有效。|  
|**pollinginterval**|**bigint**|日志扫描循环之间间隔的秒数。<br /><br /> **pollinginterval**仅对捕获作业有效。|  
|**保留**|**bigint**|更改行要在更改表中保留的分钟数。<br /><br /> **保留**仅对清除作业有效。|  
|**阀**|**bigint**|清除时可以使用一条语句删除的删除条目的最大数量。|  
  
## <a name="permissions"></a>权限  
 需要**db_owner**固定数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
 下例返回有关 `AdventureWorks2012` 数据库的已定义捕获和清除作业的信息。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_help_jobs;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
