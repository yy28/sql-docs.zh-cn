---
title: DBCC PROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DBCC PROCCACHE
- DBCC_PROCCACHE_TSQL
- PROCCACHE_TSQL
- PROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- procedure cache [SQL Server]
- displaying procedure cache information
- DBCC PROCCACHE statement
ms.assetid: 7a4f9f8a-13ff-4bf2-ba29-c17012a23659
caps.latest.revision: 31
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cce5fdd08360177c73e07a0687bd72fca6529d62
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-proccache-transact-sql"></a>DBCC PROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

以表格格式显示有关过程缓存的信息。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC PROCCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 替换为  
 允许指定其他选项。  
  
 NO_INFOMSGS  
 取消所有严重级别为 0 到 10 的信息性消息。  
  
## <a name="remarks"></a>Remarks  
使用过程缓存来缓存已编译计划和可执行计划，以加快批处理的执行速度。 过程缓存中的项处于批处理级别。 过程缓存包括以下项：
-   已编译计划  
-   执行计划  
-   Algebrizer 树  
-   扩展过程  
  
## <a name="result-sets"></a>结果集  
下表说明了结果集的各个列。
  
|列名|Description|  
|-----------------|-----------------|  
|**num proc buffs**|过程缓存中所有项使用的总页数。|  
|**num proc buffs used**|当前正在使用的所有项使用的总页数。|  
|**num proc buffs active**|仅为保持向后兼容。 当前正在使用的所有项使用的总页数。|  
|**proc cache size**|过程缓存中的总项数。|  
|**proc cache used**|当前正在使用的总项数。|  
|**proc cache active**|仅为保持向后兼容。 当前正在使用的总项数。|  
  
## <a name="permissions"></a>权限  
要求具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的成员身份。
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
