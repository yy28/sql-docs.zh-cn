---
title: sys.sp_rda_reconcile_batch (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 190c1ef35e8269cd909bfe6a8c17a7d360ae1041
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409566"
---
# <a name="syssprdareconcilebatch-transact-sql"></a>sys.sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  协调与存储在远程 Azure 表中的批处理 ID 存储在已启用延伸的 SQL Server 表中的批处理 ID。  
  
 通常只需运行**sp_rda_reconcile_batch**如果手动从远程表删除了最近迁移的数据。 在手动删除远程数据，其中包括最新的批处理，批处理 Id 不同步，然后迁移停止。  
 
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
  
## <a name="remarks"></a>Remarks  
 如果你想要删除已迁移到 Azure 的数据，执行以下操作。  
  
1.  暂停数据迁移。 有关详细信息，请参阅[暂停和恢复数据迁移 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)。  
  
2.  通过使用 STAGE_ONLY 提示运行 DELETE 命令，从 SQL Server 临时表中删除数据。 有关详细信息，请参阅[进行管理更新和删除](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints)。
  
3.  通过使用 REMOTE_ONLY 提示运行 DELETE 命令，从远程 Azure 表中删除相同的数据。  
  
4.  运行**sp_rda_reconcile_batch**。  
  
5.  恢复数据迁移。 有关详细信息，请参阅[暂停和恢复数据迁移 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)。  
  
## <a name="example"></a>示例  
 若要对帐批 Id，请运行以下语句。  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
