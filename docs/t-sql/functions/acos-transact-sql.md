---
title: ACOS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ACOS
- ACOS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cosine
- ACOS function
- arccosine
ms.assetid: 4ec6b46e-9438-4f0f-8b96-461edd84280a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 262b89b15100a5e79fba5626c4cf7cfc890ecaac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948224"
---
# <a name="acos-transact-sql"></a>ACOS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

一个函数，返回以弧度表示的角，其正弦为指定的 float 表达式。 也称为反余弦。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
ACOS ( float_expression )  
```  
  
## <a name="arguments"></a>参数  
*float_expression*  
float 类型或可隐式转换为 float 类型的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)  。 仅介于 -1.00 到 1.00 之间的值有效。 对于超出此范围的值，将返回 NULL 且 ASIN 将报告域错误。
  
## <a name="return-types"></a>返回类型  
**float**
  
## <a name="examples"></a>示例  
此示例返回指定数量的 `ACOS` 的值。
  
```sql
SET NOCOUNT OFF;  
DECLARE @cos float;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(varchar, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[数学函数 (Transact-SQL)](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[函数](../../t-sql/functions/functions.md)
  
  

