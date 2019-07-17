---
title: 变更数据捕获存储的过程 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], change data capture
- change data capture [SQL Server], stored procedures
ms.assetid: 7da7068d-6388-465a-b708-a2f27ded1efe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 128d62aceec5a847e721d6227372e1ff115706ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078230"
---
# <a name="change-data-capture-stored-procedures-transact-sql"></a>更改数据捕获存储过程 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  变更数据捕获使得在启用表上发生的数据操纵语言 (DML) 活动的历史记录能够以方便的关系格式提供。 使用以下存储过程可以配置变更数据捕获、管理变更数据捕获代理作业和为更改数据使用者提供当前元数据。  
  
|||  
|-|-|  
|[sys.sp_cdc_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)|[sys.sp_cdc_generate_wrapper_function &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)|  
|[sys.sp_cdc_change_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)|[sys.sp_cdc_get_captured_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)|  
|[sys.sp_cdc_cleanup_change_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-cleanup-change-table-transact-sql.md)|[sys.sp_cdc_get_ddl_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)|  
|[sys.sp_cdc_disable_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)|[sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)|  
|[sys.sp_cdc_disable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)|[sys.sp_cdc_help_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)|  
|[sys.sp_cdc_drop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)|[sys.sp_cdc_scan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)|  
|[sys.sp_cdc_enable_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)|[sys.sp_cdc_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)|  
|[sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)|[sys.sp_cdc_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)|  
  
## <a name="see-also"></a>请参阅  
 [更改数据捕获表&#40;Transact SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)  
  
  
