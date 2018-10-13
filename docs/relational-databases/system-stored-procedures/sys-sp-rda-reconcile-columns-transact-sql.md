---
title: sys.sp_rda_reconcile_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4d2a8377466876270bcedd07138cf9cf30ef211
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48906317"
---
# <a name="syssprdareconcilecolumns-transact-sql"></a>sys.sp_rda_reconcile_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  协调远程 Azure 表中的列到已启用延伸的 SQL Server 表中的列。  
    
  **sp_rda_reconcile_columns**将列添加到已启用延伸的 SQL Server 表中但在远程表中不存在的远程表。 这些列可能意外地删除远程表中的列。 但是， **sp_rda_reconcile_columns**不会从远程表中但在 SQL Server 表中不存在的远程表中删除列。
  
  > [!IMPORTANT]
  > 当 **sp_rda_reconcile_columns** 重新创建你从远程表中意外删除的列时，不会还原之前位于已删除列中的数据。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>语法  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>参数  
 \@objname = '*\@objname*  
 已启用延伸的 SQL Server 表的名称。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0（失败）  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 权限。  
   
## <a name="remarks"></a>备注  
 如果远程 Azure 表中存在已启用延伸的 SQL Server 表中不复存在的列，这些额外的列不会阻止 Stretch Database 正常运行。 你可以选择手动删除额外列。  
  
## <a name="example"></a>示例  
 若要对帐远程 Azure 表中的列，请运行以下语句。  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
