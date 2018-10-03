---
title: sys.sysaltfiles (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysaltfiles_TSQL
- sys.sysaltfiles
- sysaltfiles_TSQL
- sysaltfiles
dev_langs:
- TSQL
helpviewer_keywords:
- sysaltfiles system table
- sys.sysaltfiles compatibility view
ms.assetid: 698dec23-5336-4108-87a5-f8e407f8da09
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 941b51b6e05fd88a8b59b8e4f3b28ee145affe3d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636555"
---
# <a name="syssysaltfiles-transact-sql"></a>sys.sysaltfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在特殊情况下，包含与数据库中的文件相对应的行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|文件标识号。 它对每个数据库都是唯一的。|  
|**groupid**|**smallint**|文件组标识号。|  
|size|**int**|文件大小（以 8 KB 页为单位）。|  
|**最大大小**|**int**|最大文件大小（以 8 KB 为单位的页）。<br /><br /> 0 = 无增长。<br /><br /> -1 = 文件将一直增长到磁盘充满为止。<br /><br /> 268435456 = 日志文件将增长到最大大小 2 TB。<br /><br /> 注意： 如果升级的无限制的日志文件大小的数据库将报告为-1 日志文件的最大大小。|  
|**增长**|**int**|数据库的增长大小。<br /><br /> 0 = 无增长。 根据状态的值，可以是页数或文件大小的百分比。 如果**状态**为 0x100000，**增长**所占的百分比文件大小; 否则为，它的页数。|  
|**status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**perf**|**int**|保留。|  
|**dbid**|**smallint**|该文件所属数据库的数据库标识号。|  
|**名称**|**sysname**|文件的逻辑名称。|  
|**filename**|nvarchar(260)|物理设备的名称。 这包括文件的完整路径。|  
  
## <a name="see-also"></a>请参阅  
 [系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
