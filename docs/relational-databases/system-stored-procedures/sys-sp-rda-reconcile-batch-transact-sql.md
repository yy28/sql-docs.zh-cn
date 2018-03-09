---
title: sys.sp_rda_reconcile_batch (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1df76c9b3107b5fbd45eb8a99eab1ec5baf5f4ee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="syssprdareconcilebatch-transact-sql"></a>sys.sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  协调与远程 Azure 表中存储的批处理 ID 存储在已启用延伸的 SQL Server 表中的批处理 ID。  
  
 通常只需运行**sp_rda_reconcile_batch**如果你已手动删除远程表中的最近迁移的数据。 在您手动删除远程数据，包括最新的批处理，批处理 Id 是同步的然后迁移停止。  
 
 若要删除已迁移到 Azure 的数据，请参阅此页上的备注部分。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>语法  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>参数  
 @objname = '*@objname*'  
 已启用延伸的 SQL Server 表的名称。  
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
  
## <a name="remarks"></a>注释  
 如果你想要删除已迁移到 Azure 的数据，执行以下操作。  
  
1.  暂停数据迁移。 有关详细信息，请参阅[暂停和恢复数据迁移 &#40;Stretch Database &#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
2.  通过使用 STAGE_ONLY 提示中运行删除命令，从 SQL Server 临时表中删除数据。 有关详细信息，请参阅[进行管理更新和删除](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints)。
  
3.  通过使用 REMOTE_ONLY 提示中运行删除命令，从远程 Azure 表中删除相同的数据。  
  
4.  运行**sp_rda_reconcile_batch**。  
  
5.  恢复数据迁移。 有关详细信息，请参阅[暂停和恢复数据迁移 &#40;Stretch Database &#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
## <a name="example"></a>示例  
 若要先对帐批处理 Id，请运行以下语句。  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
