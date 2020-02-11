---
title: sys. sysdevices （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdevices
- sysdevices_TSQL
- sys.sysdevices
- sys.sysdevices_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdevices compatibility view
- sysdevices system table
ms.assetid: ac5bcaf4-8fb6-4855-8856-d7643f469361
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cbd14a7ce8dd1cfb1571874a83a615065200014
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053519"
---
# <a name="syssysdevices-transact-sql"></a>sys.sysdevices (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个磁盘备份文件、磁带备份文件和数据库文件在表中对应一行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**路径名**|**sysname**|备份文件或数据库文件的逻辑名称。|  
|**规格**|**int**|以两千字节 (KB) 页为单位的文件大小。|  
|**低级**|**int**|维护该列只是为了向后兼容。|  
|**严重**|**int**|维护该列只是为了向后兼容。|  
|**状态值**|**smallint**|指示设备类型的位图：<br /><br /> 1 = 默认磁盘<br /><br /> 2 = 物理磁盘<br /><br /> 4 = 逻辑磁盘<br /><br /> 8 = 跳过标头<br /><br /> 16 = 备份文件<br /><br /> 32 = 串行写<br /><br /> 4096 = 只读|  
|**cntrltype**|**smallint**|控制器类型：<br /><br /> 0 = 非 CD-ROM 数据库文件<br /><br /> 2 = 磁盘备份文件<br /><br /> 3 - 4 = 软盘备份文件<br /><br /> 5 = 磁带备份文件<br /><br /> 6 = 命名管道文件|  
|**phyname**|**nvarchar(260)**|物理文件的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;的兼容性视图 &#40;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
