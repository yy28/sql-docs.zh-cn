---
title: sp_xtp_flush_temporal_history | Microsoft Docs
ms.custom: 
ms.date: 02/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
f1_keywords:
- sp_xtp_flush_temporal_history
- sp_xtp_flush_temporal_history_TSQL
- sys.sp_xtp_flush_temporal_history
- sys.sp_xtp_flush_temporal_history_TSQL
helpviewer_keywords:
- sp_xtp_flush_temporal_history
ms.assetid: 322e3170-93f8-468a-a123-104ce7bd7fad
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f68bb1a07ba3edb33c99339b53b0f85e343576ad
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="temporal-table---spxtpflushtemporalhistory"></a>临时表的 sp_xtp_flush_temporal_history
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  调用数据刷新任务来从内存中临时表的所有已提交的行移到基于磁盘的历史记录表。  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_xtp_flush_temporal_history @schema_name, @object_name  
  
```  
  
## <a name="arguments"></a>参数  
 *@schema_name*  
 当前表或临时表架构名称  
  
 *@object_name*  
 当前或临时表的名称  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0（失败）  
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
  
## <a name="see-also"></a>另请参阅  
 [内存优化系统版本控制临时表的性能注意事项](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)  
  
  
