---
title: sys. sp_rda_set_rpo_duration (Transact-sql) |Microsoft Docs
description: 了解 sys.databases. sp_rda_set_rpo_duration。 使用此存储过程设置 SQL Server 保留在临时表中的已迁移数据的小时数。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d37717f2b2c8a3dad804538a9268e64023776422
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540435"
---
# <a name="syssp_rda_set_rpo_duration-transact-sql"></a>sys. sp_rda_set_rpo_duration (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  设置 SQL Server 保留在临时表中的已迁移数据的小时数，以帮助确保远程 Azure 数据库完整还原（如果需要进行时间点还原）。    
    
 有关详细信息，请参阅 [Stretch Database 通过暂时保留已迁移行来降低 Azure 数据的数据丢失风险](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>语法    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>参数    
 [ @duration_hrs =] *duration_hrs*    
 是要 SQL Server 为当前已启用延伸的数据库保留的已迁移数据)  (非 null 整数值的小时数。 默认值和最小值为8小时。    
 
 > [!NOTE]
 > 较高的值需要 SQL Server 上的更多存储空间。
    
## <a name="permissions"></a>权限    
 需要 db_owner 权限。    
    
## <a name="remarks"></a>备注    
 通过运行 [sp_rda_get_rpo_duration &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)获取当前值。    
    
## <a name="see-also"></a>另请参阅    
 [sys. sp_rda_get_rpo_duration &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [还原已启用延伸的数据库 (Stretch Database) ](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)    
    
  
