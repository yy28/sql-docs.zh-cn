---
title: cdc. lsn_time_mapping （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 417e57b6872ca5b54f7acefb28f65b2652f41da7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758689"
---
# <a name="cdclsn_time_mapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  为每个在更改表中存在行的事务返回一行。 该表用于在日志序列号 (LSN) 提交值和提交事务的时间之间建立映射。 没有对应的更改表项的项也可以记录下来， 以便表在变更活动少或者无变更活动期间将 LSN 处理的完成过程记录下来。  
  
 我们建议您不要直接查询系统表， 请改为执行[fn_cdc_map_lsn_to_time &#40;transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)和[sys. fn_cdc_map_time_to_lsn &#40;transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)系统函数。  
    
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|提交的事务的 LSN。|  
|**tran_begin_time**|**datetime**|与 LSN 关联的事务开始的时间。|  
|**tran_end_time**|**datetime**|事务结束的时间。|  
|**tran_id**|**varbinary （10）**|事务的 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [事务日志 (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [&#60;capture_instance&#62;_CT &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
