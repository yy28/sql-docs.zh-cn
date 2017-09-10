---
title: "DBCC FREESYSTEMCACHE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70de1caf9d8bceab6b596952044bb7b3961f60f2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

从所有缓存中释放所有未使用的缓存条目。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]会事先在后台清理未使用的缓存条目，以使内存可用于当前条目。 但是，可以使用此命令从所有缓存中或者从指定的资源调控器池缓存中手动删除未使用的条目。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
```sql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>参数  
 ('ALL' [，*pool_name* ])  
 ALL 指定所有受支持的缓存。  
 *pool_name*指定资源调控器池缓存。 只释放与此池关联的条目。  
  
 MARK_IN_USE_FOR_REMOVAL  
 当不再使用当前使用的条目后，将它们分别从其各自所属的缓存中进行异步释放。 当 DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL 执行后，缓存中新创建的条目不会受到影响。  
  
 NO_INFOMSGS  
 取消显示所有信息性消息。  
  
## <a name="remarks"></a>注释  
执行 DBCC FREESYSTEMCACHE 将清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计划缓存。 清除计划缓存将导致对所有后续执行计划进行重新编译，并可能导致查询性能暂时性地突然降低。 对于计划缓存中每个已清除的缓存存储区，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志将包含以下信息性消息：“由于 'DBCC FREEPROCCACHE' 或 'DBCC FREESYSTEMCACHE' 操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 经历了 '%s' 缓存存储区(计划缓存的一部分)的 %d 次刷新。” 每隔五分钟，只要缓存在这段时间间隔内得到刷新，此消息就记录一次。

## <a name="result-sets"></a>结果集  
DBCC FREESYSTEMCACHE 返回:"DBCC 执行完毕。 如果 DBCC 输出了错误消息，请与系统管理员联系。”
  
## <a name="permissions"></a>Permissions  
需要对服务器的 ALTER SERVER STATE 权限。
  
## <a name="examples"></a>示例  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. 从资源调控器池缓存释放未使用的缓存条目  
下面的示例说明如何清除专属于某个指定资源调控器资源池的缓存。
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. 当不再使用条目后，将它们分别从其各自所属的缓存中释放  
下面的示例使用 MARK_IN_USE_FOR_REMOVAL 子句，在不再使用条目后将它们从所有当前缓存中释放。
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[资源调控器](../../relational-databases/resource-governor/resource-governor.md)
  
  

