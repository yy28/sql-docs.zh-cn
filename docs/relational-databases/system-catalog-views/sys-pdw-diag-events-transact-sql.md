---
title: sys.pdw_diag_events (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 59bb3e9c-2829-49a0-b382-652ed1f54f88
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3c7cb2aaf1fac585514c4d7e540c35c1f44fad1b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987220"
---
# <a name="syspdwdiagevents-transact-sql"></a>sys.pdw_diag_events (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存在系统上的诊断会话中可以包含事件有关的信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|**名称**|**nvarchar(255)**|特定诊断事件的名称。||  
|**源 (source)**|**nvarchar(255)**|事件 （引擎、 常规、 dms 等） 的源||  
|**is_enabled**|**bit**|是否正在发布事件。||  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
