---
title: fn_trace_getdata （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 8f342fd9dcf89b5d9862a2ed51718b09aae2e991
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771529"
---
# <a name="snapshotsfn_trace_getdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  该函数返回为指定跟踪捕获的所有事件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>自变量  
 *trace_info_id*  
 快照中主键的唯一标识符。管理数据仓库数据库中的 trace_info 表。 *trace_info_id*是**int**。  
  
 *start_time*  
 跟踪的开始时间。 *start_time*为**日期时间**。  
  
 *end_time*  
 跟踪的结束时间。 *end_time*为**日期时间**。  
  
## <a name="table-returned"></a>返回的表  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|\<All trace columns>|\<Varies>|来自管理数据仓库数据库中 snapshots.trace_info 表的跟踪数据。<br /><br /> 可通过使用以下查询来获取指定跟踪的列的列表：<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **注意：** 由快照返回的列。 fn_trace_gettable 函数与 sys.databases trace_columns 系统视图中 "名称" 列中的值相对应。 唯一的差别在于该函数不返回 GroupID 列。|  
  
## <a name="permissions"></a>权限  
 要求拥有 mdw_reader 的 SELECT 权限。  
  
## <a name="see-also"></a>另请参阅  
 [数据收集](../../relational-databases/data-collection/data-collection.md)  
  
  
