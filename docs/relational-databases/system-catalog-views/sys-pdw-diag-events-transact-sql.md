---
title: sys.pdw_diag_events (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 59bb3e9c-2829-49a0-b382-652ed1f54f88
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4aa83c4931e1cce4b4b813baa489ae43798db594
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127555"
---
# <a name="syspdwdiagevents-transact-sql"></a>sys.pdw_diag_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存在系统上的诊断会话中可以包含事件有关的信息。  
  
|列名|数据类型|描述|范围|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|特定诊断事件的名称。||  
|**源 (source)**|**nvarchar(255)**|事件 （引擎、 常规、 dms 等） 的源||  
|**is_enabled**|**bit**|是否正在发布事件。||  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
