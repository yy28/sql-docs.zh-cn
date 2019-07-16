---
title: sys.sysperfinfo (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
author: rothja
ms.author: jroth
ms.openlocfilehash: e6ce86e7be7d54e95c2336691b53ea12ff0d8575
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076497"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]可通过 Windows 系统监视器显示的内部性能计数器的表示形式。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|性能对象名称，如**SQLServer:LockManager**或**SQLServer:BufferManager**。|  
|**counter_name**|**nchar(128)**|在对象中的性能计数器名称如**页面请求**或**Locks Requested**。|  
|**instance_name**|**nchar(128)**|计数器的命名实例。 例如，有每种类型的锁，如维护的计数器**表**，**页面**，**密钥**，依次类推。 实例名在相似的计数器之间是有区别的。|  
|**cntr_value**|**bigint**|实际计数器值。 通常，该值是一个级别或对实例事件发生进行计数的单调递增计数器。|  
|**cntr_type**|**int**|Windows 性能体系结构定义的计数器类型。|  
  
## <a name="see-also"></a>请参阅  
 [系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
