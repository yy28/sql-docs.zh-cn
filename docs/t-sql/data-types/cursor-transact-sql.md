---
title: "游标 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b0b96a3bc147f51102fa10f2dff96b7f1761759
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="cursor-transact-sql"></a>cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

这是变量或存储过程 OUTPUT 参数的一种数据类型，这些参数包含对游标的引用。
  
## <a name="remarks"></a>注释  
可引用变量和参数具有的操作**光标**数据类型为：
-   DECLARE  *@local_variable*  ，并且已设置 *@local_variable* 语句。  
-   OPEN、FETCH、CLOSE 及 DEALLOCATE 游标语句。  
-   存储过程输出参数。  
-   CURSOR_STATUS 函数。  
-   **Sp_cursor_list**， **sp_describe_cursor**， **sp_describe_cursor_tables**，和**sp_describe_cursor_columns**系统存储过程。  
  
**Cursor_name**输出列的**sp_cursor_list**和**sp_describe_cursor**返回游标变量的名称。
  
使用创建的任何变量**光标**数据类型都可以为 null。
  
**光标**数据类型不能用于 CREATE TABLE 语句中的列。
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40;Transact SQL &#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[声明光标 &#40;Transact SQL &#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

