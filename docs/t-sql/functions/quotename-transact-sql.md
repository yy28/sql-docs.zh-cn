---
title: "QUOTENAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUOTENAME_TSQL
- QUOTENAME
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- input strings [SQL Server]
- Unicode [SQL Server], delimited identifiers
- QUOTENAME function
- valid identifiers [SQL Server]
ms.assetid: 34d47f1e-2ac7-4890-8c9c-5f60f115e076
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f4e40797fc49e8a70b01162fc6959ad60475e8b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="quotename-transact-sql"></a>QUOTENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回带有分隔符的 Unicode 字符串，分隔符的加入可使输入的字符串成为有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔标识符。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
## <a name="arguments"></a>参数  
 *character_string*  
 Unicode 字符数据构成的字符串。 *character_string*是**sysname**且最多 128 个字符。 超过 128 个字符的输入将返回 NULL。  
  
 *quote_character*  
 用作分隔符的单字符字符串。 可以是单引号 (  )，左或向右括号 ( **[]** )，或双引号 ( **"** )。 如果*quote_character*未指定，则使用方括号。  
  
## <a name="return-types"></a>返回类型  
 **nvarchar(258)**  
  
## <a name="examples"></a>示例  
 以下示例接受字符串 `abc[]def` 并使用 `[` 和 `]` 字符来创建有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔标识符。  
  
```  
SELECT QUOTENAME('abc[]def');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]  
  
(1 row(s) affected)  
```  
  
 请注意，字符串 `abc[]def` 中的右方括号有两个，用于指示转义符。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例接受字符串 `abc def` 并使用 `[` 和 `]` 字符来创建有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔标识符。  
  
```  
SELECT QUOTENAME('abc def');   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc def]  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


