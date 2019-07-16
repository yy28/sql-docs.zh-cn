---
title: snapshots.fn_trace_getdata (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- snapshots.fn_trace_getdata
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots.fn_trace_getdata function
ms.assetid: ac28ef48-f4f4-4bf2-ba22-d44e1be88172
author: rothja
ms.author: jroth
ms.openlocfilehash: a85a911d4c9f5cd4565e9839f3be44a4e2366079
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067756"
---
# <a name="snapshotsfntracegetdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  该函数返回为指定跟踪捕获的所有事件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>参数  
 *trace_info_id*  
 中管理数据中 snapshots.trace_info 表的主键的唯一标识符的仓库数据库。 *trace_info_id*是**int**。  
  
 *start_time*  
 跟踪的开始时间。 *start_time*是**datetime**。  
  
 *end_time*  
 跟踪的结束时间。 *end_time*是**datetime**。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|\<所有跟踪列 >|\<各不相同 >|来自管理数据仓库数据库中 snapshots.trace_info 表的跟踪数据。<br /><br /> 可通过使用以下查询来获取指定跟踪的列的列表：<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **注意：** Snapshots.fn_trace_gettable 函数返回的列与 sys.trace_columns 系统视图中的名称列中的值相对应。 唯一的差别在于该函数不返回 GroupID 列。|  
  
## <a name="permissions"></a>权限  
 要求拥有 mdw_reader 的 SELECT 权限。  
  
## <a name="see-also"></a>请参阅  
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)  
  
  
