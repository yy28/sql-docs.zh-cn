---
description: 'sp_xtp_flush_temporal_history (Transact-sql) '
title: sp_xtp_flush_temporal_history |Microsoft Docs
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_xtp_flush_temporal_history
- sp_xtp_flush_temporal_history_TSQL
- sys.sp_xtp_flush_temporal_history
- sys.sp_xtp_flush_temporal_history_TSQL
helpviewer_keywords:
- sp_xtp_flush_temporal_history
ms.assetid: 322e3170-93f8-468a-a123-104ce7bd7fad
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ead5aae7b27528c12c4d44d574106815ddf382f5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473320"
---
# <a name="sp_xtp_flush_temporal_history-transact-sql"></a>sp_xtp_flush_temporal_history (Transact-sql) 
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  调用数据刷新任务，将所有提交的行从内存中的临时表移到基于磁盘的历史记录表。  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_xtp_flush_temporal_history @schema_name, @object_name  
  
```  
  
## <a name="arguments"></a>参数  
 *\@schema_name*  
 当前表或临时表的架构名称  
  
 *\@object_name*  
 当前表或临时表的名称  
  
## <a name="return-code-values"></a>返回代码值  
 0 (成功) 或 >0 (故障)   
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
  
## <a name="see-also"></a>另请参阅  
 [内存优化系统版本控制临时表的性能注意事项](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)  
  
  
