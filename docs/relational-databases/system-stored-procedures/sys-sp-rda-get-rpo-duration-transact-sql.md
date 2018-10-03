---
title: sys.sp_rda_get_rpo_duration (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0882344345c315f13d6cca11b7a1d1db88c9417b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769695"
---
# <a name="syssprdagetrpoduration-transact-sql"></a>sys.sp_rda_get_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  获取在临时表以帮助确保完整还原的远程 Azure 数据库，如果时间还原点是必需的 SQL Server 保留的已迁移数据的小时数。 
  
  有关详细信息，请参阅[Stretch Database 通过暂时保留已迁移的行来降低你的 Azure 数据的数据丢失的风险](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)。  
    
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>语法    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>输出参数    
 *@durationinhours*    
  是的小时数 （非 null 的整数值） 的 SQL Server 可在保留当前已启用延伸的数据库的已迁移数据。    
    
## <a name="permissions"></a>Permissions    
 需要 db_owner 权限。    
    
## <a name="remarks"></a>备注    
 通过运行更改该值[sys.sp_rda_set_rpo_duration &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)。    
    
## <a name="see-also"></a>请参阅    
 [sys.sp_rda_set_rpo_duration &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [还原已启用延伸的数据库 (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)    
    
  
