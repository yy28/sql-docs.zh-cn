---
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 24316c384dbf8f7074a852dfce8ff8358321eb06
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="changetrackingiscolumninmask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  用于解释由 CHANGETABLE(CHANGES …) 函数返回的 SYS_CHANGE_COLUMNS 值。 这使应用程序能够确定指定的列是否包含在为 SYS_CHANGE_COLUMNS 返回的值中。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>参数  
 *column_id*  
 是正在被检查的列的 ID。 可以通过获取 ID 列[COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)函数。  
  
 *change_columns*  
 是从 SYS_CHANGE_COLUMNS 列中的二进制数据[CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)数据。  
  
## <a name="return-type"></a>返回类型  
 **bit**  
  
## <a name="return-values"></a>返回值  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK 返回下列值。  
  
|返回值|Description|  
|------------------|-----------------|  
|0|指定的列不在*change_columns*列表。|  
|1|指定的该列包含在*change_columns*列表。|  
  
## <a name="remarks"></a>注释  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK 不执行任何检查来验证*column_id*值或*change_columns*参数已从从中的表获取*column_id*获得。  
  
## <a name="examples"></a>示例  
 下面的示例确定是否已更新 `Salary` 表的 `Employees` 列。 `COLUMNPROPERTY`函数返回的列 ID`Salary`列。 必须使用 CHANGETABLE 作为数据源将 `@change_columns` 局部变量设置为查询的结果。  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>另请参阅  
 [变更跟踪函数 (Transact-SQL)](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE (Transact-SQL)](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [跟踪数据更改 (SQL Server)](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
