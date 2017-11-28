---
title: "sys.syscacheobjects (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscacheobjects_TSQL
- sys.syscacheobjects
- syscacheobjects
- syscacheobjects_TSQL
dev_langs: TSQL
helpviewer_keywords:
- syscacheobjects system table
- sys.syscacheobjects compatibility view
ms.assetid: 9b14f37c-b7f5-4f71-b070-cce89a83f69e
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9925669bec972d543b6dc688d19a5dab25db032c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syssyscacheobjects-transact-sql"></a>sys.syscacheobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含有关如何使用缓存的信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**bucketid**|**int**|存储桶 ID。 该值表示从 0 到（目录大小 - 1）的范围。 目录大小为哈希表的大小。|  
|**cacheobjtype**|**nvarchar(17)**|缓存中的对象类型：<br /><br /> 编译计划<br /><br /> 可执行计划<br /><br /> 分析树<br /><br /> 游标<br /><br /> 扩展存储过程|  
|**objtype**|**nvarchar （8)**|对象的类型：<br /><br /> 存储过程<br /><br /> 预定义语句<br /><br /> 即席查询 ([!INCLUDE[tsql](../../includes/tsql-md.md)]作为语言事件提交**sqlcmd**或**osql**实用程序，而不是远程过程调用)<br /><br /> ReplProc（复制过程）<br /><br /> 触发器<br /><br /> 视图<br /><br /> 默认<br /><br /> 用户表<br /><br /> 系统表<br /><br /> 检查<br /><br /> 规则|  
|**objid**|**int**|用于在缓存中查找对象的主键之一。 这是的对象 ID 存储在**sysobjects**的数据库对象 （过程、 视图、 触发器和等等）。 如即席或已准备 SQL 的缓存对象**objid**是一个内部生成的值。|  
|**dbid**|**int**|在其中编译缓存对象的数据库 ID。|  
|**dbidexec**|**int**|执行查询的数据库 ID。<br /><br /> 对于大多数对象， **dbidexec**具有相同的值**dbid**。<br /><br /> 对于系统视图， **dbidexec**是从其执行查询的数据库 ID。<br /><br /> 针对即席查询**dbidexec**为 0。 这意味着**dbidexec**具有相同的值**dbid**。|  
|**uid**|**int**|表示特殊查询计划和已准备好的计划的计划创建者。<br /><br /> -2 = 提交的批处理不依赖于隐式名称解析并可在不同的用户间共享。 这是首选方法。 任何其他值表示数据库中提交查询的用户的用户 ID。<br /><br /> 如果用户数和角色数超过 32,767，则发生溢出或返回 NULL。|  
|**refcounts**|**int**|引用该缓存对象的其他缓存对象数。 计数 1 为基数。|  
|**usecounts**|**int**|自开始以来使用该缓存对象的次数。|  
|**pagesused**|**int**|缓存对象占用的页数。|  
|**setopts**|**int**|影响编译计划的 SET 选项设置。 这些设置是缓存键的一部分。 该列中的值更改表示用户已修改了 SET 选项。 这些选项包括：<br /><br /> **ANSI_PADDING**<br /><br /> **FORCEPLAN**<br /><br /> **CONCAT_NULL_YIELDS_NULL**<br /><br /> **ANSI_WARNINGS**<br /><br /> **ANSI_NULLS**<br /><br /> **QUOTED_IDENTIFIER**<br /><br /> **ANSI_NULL_DFLT_ON**<br /><br /> **ANSI_NULL_DFLT_OFF**|  
|**langid**|**int**|语言 ID。 创建缓存对象的连接的语言 ID。|  
|**dateformat**|**int**|创建缓存对象的连接的日期格式。|  
|**status**|**int**|表示缓存对象是否是游标计划。 目前只使用最小的有效位。|  
|**lasttime**|**bigint**|仅为保持向后兼容。 始终返回 0。|  
|**maxexectime**|**bigint**|仅为保持向后兼容。 始终返回 0。|  
|**avgexectime**|**bigint**|仅为保持向后兼容。 始终返回 0。|  
|**lastreads**|**bigint**|仅为保持向后兼容。 始终返回 0。|  
|**lastwrites**|**bigint**|仅为保持向后兼容。 始终返回 0。|  
|**对**|**int**|过程定义或提交的批处理的长度（以字节为单位）。|  
|**sql**|**nvarchar(3900)**|模块定义或提交的批处理的前 3900 个字符。|  
  
## <a name="see-also"></a>另请参阅  
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

