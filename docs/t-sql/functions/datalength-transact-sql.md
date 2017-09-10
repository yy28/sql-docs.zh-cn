---
title: "Datalength 之外 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49889c4b29de0d86859c1363ce13b9656645848d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回用于表示任何表达式的字节数。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>参数  
*expression*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何数据类型。
  
## <a name="return-types"></a>返回类型
**bigint**如果*表达式*的**varchar （max)**， **nvarchar (max)**或**varbinary （max)**数据类型;否则为**int**。
  
## <a name="remarks"></a>注释  
Datalength 之外是尤其有用**varchar**， **varbinary**，**文本**，**映像**， **nvarchar**，和**ntext**数据类型，因为这些数据类型可以存储长度可变的数据。
  
NULL 的 DATALENGTH 的结果是 NULL。
  
> [!NOTE]  
>  兼容级别可能影响返回值。 有关兼容性级别的详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="examples"></a>示例  
下面的示例查找 `Name` 表中的 `Product` 列的长度。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT length = DATALENGTH(Name), Name  
FROM Production.Product  
ORDER BY Name;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
下面的示例查找 `Name` 表中的 `Product` 列的长度。
  
```sql
-- Uses AdventureWorks  
  
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[LEN &#40;Transact SQL &#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[系统函数 &#40;Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  


