---
title: （除法赋值）(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- /=_TSQL
- /=
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, /=
- assignment operators, /=
- augmented operators, /=
- /= (divide equals)
ms.assetid: 9ab25d1e-5c98-4dd7-b2cd-9f49499c86e7
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: df1840c0b97dcf43703e5d5fec447923af9265c9
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55046171"
---
# <a name="-division-assignment-transact-sql"></a>/=（除法赋值）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  将一个数除以另一个数并将值设置为运算的结果。 例如，如果变量 @x 等于 34，则 `@x /= 2` 会将 @x 的原始值除以 2 并将 @x 设置为该新值 (17)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression /= expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 数值类别中任意数据类型（bit 数据类型除外）的任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="result-types"></a>结果类型  
 返回优先级较高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 有关详细信息，请参阅[（除法）(Transact-SQL)](../../t-sql/language-elements/divide-transact-sql.md)。  

## <a name="examples"></a>示例  
以下示例将一个变量设置为 17， 然后使用 `/=` 运算符将该变量设置为其原始值的一半。  
```sql  
DECLARE @myVariable decimal(5,2);
SET @myVariable = 17.5;
SET @myVariable /= 2;
SELECT @myVariable AS ResultVariable;  
```
  
[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]  

|ResultVariable | 
|--- |
|8.75 |

## <a name="see-also"></a>另请参阅  
 [复合运算符 (Transact-SQL)](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
