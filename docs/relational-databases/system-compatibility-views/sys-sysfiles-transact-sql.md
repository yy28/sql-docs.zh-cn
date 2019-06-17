---
title: sys.sysfiles (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c2c139a914b511ab7ee80a0fdd180bab5654205a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047130"
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  数据库中的每个文件对应一行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|每个数据库的唯一文件标识号。|  
|**groupid**|**smallint**|文件组标识号。|  
|size |**int**|文件大小（8 KB 页）。|  
|**maxsize**|**int**|最大文件大小（以 8 KB 为单位的页）。<br /><br /> 0 = 无增长。<br /><br /> -1 = 文件将一直增长到磁盘充满为止。<br /><br /> 268435456 = 日志文件将增长到最大大小 2 TB。<br /><br /> 注意：如果升级的无限制的日志文件大小的数据库将报告为-1 日志文件的最大大小。|  
|**growth**|**int**|数据库的增长大小。 可以是页数或文件大小，具体取决于值的百分比**状态**。<br /><br /> 0 = 无增长。|  
|**status**|**int**|状态位**增长**兆字节 (MB) 或千字节 (KB) 中的值。<br /><br /> 0x2 = 磁盘文件。<br /><br /> 0x40 = 日志文件。<br /><br /> 0x100000 = 增长。 该值是百分比，不是页数。|  
|**perf**|**int**|保留。|  
|**名称**|**sysname**|文件的逻辑名称。|  
|**filename**|nvarchar(260) |物理设备的名称。 这包括文件的完整路径。|  
  
## <a name="see-also"></a>请参阅  
 [系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
