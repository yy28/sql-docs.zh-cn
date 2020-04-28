---
title: sys. sp_rda_reconcile_columns （Transact-sql） |Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7ad2fd6c51f5b5463e4e4c10745b2ff245bd691d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083672"
---
# <a name="syssp_rda_reconcile_columns-transact-sql"></a>sys. sp_rda_reconcile_columns （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  将远程 Azure 表中的列与启用 Stretch SQL Server 表中的列协调。  
    
  **sp_rda_reconcile_columns**将列添加到已启用 Stretch SQL Server 表中但不在远程表中的远程表中。 这些列可能是您意外从远程表中删除的列。 但是， **sp_rda_reconcile_columns**不会删除远程表中存在的远程表中的列，而不会删除 SQL Server 表中的列。
  
  > [!IMPORTANT]
  > 当 **sp_rda_reconcile_columns** 重新创建你从远程表中意外删除的列时，不会还原之前位于已删除列中的数据。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>语法  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>参数  
 \@objname = '*\@objname*'  
 已启用延伸的 SQL Server 表的名称。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0 （失败）  
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
   
## <a name="remarks"></a>备注  
 如果远程 Azure 表中存在已启用延伸的 SQL Server 表中不复存在的列，这些额外的列不会阻止 Stretch Database 正常运行。 你可以选择手动删除额外列。  
  
## <a name="example"></a>示例  
 若要协调远程 Azure 表中的列，请运行以下语句。  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
