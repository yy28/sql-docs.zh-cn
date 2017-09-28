---
title: "空间 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SPACE_TSQL
- SPACE
dev_langs:
- TSQL
helpviewer_keywords:
- strings [SQL Server], repeated spaces
- repeated spaces
- SPACE function
ms.assetid: b4fac3b8-2d47-4c11-a6a6-009e5a538f40
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f5de41d3d7619af5f83fa2bee8cd30f980f291b7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="space-transact-sql"></a>SPACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回由重复空格组成的字符串。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SPACE ( integer_expression )  
```  
  
## <a name="arguments"></a>参数  
 *integer_expression*  
 指示空格个数的正整数。 如果*integer_expression*为负，则返回一个 null 字符串。  
  
 有关详细信息，请参阅[表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
## <a name="return-types"></a>返回类型  
 **varchar**  
  
## <a name="remarks"></a>注释  
 若要在 Unicode 数据中包括空格或返回 8000 个以上的字符空格，请使用 REPLICATE 而不是 SPACE。  
  
## <a name="examples"></a>示例  
 以下示例剪裁姓氏，并将逗号、两个空格和 `Person` 中的 `AdventureWorks2012` 表列出的人员名字串联起来。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT RTRIM(LastName) + ',' + SPACE(2) +  LTRIM(FirstName)  
FROM Person.Person  
ORDER BY LastName, FirstName;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例剪裁姓氏，并将逗号、两个空格和 `DimCustomer` 中的 `AdventureWorksPDW2012` 表列出的人员名字串联起来。  
  
```  
-- Uses AdventureWorks  
  
SELECT RTRIM(LastName) + ',' + SPACE(2) +  LTRIM(FirstName)  
FROM dbo.DimCustomer  
ORDER BY LastName, FirstName;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [复制 &#40;Transact SQL &#41;](../../t-sql/functions/replicate-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)  
  
  



