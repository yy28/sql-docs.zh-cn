---
title: "反斜杠 （续行符） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- '\_TSQL'
- '\'
dev_langs: TSQL
helpviewer_keywords:
- backwhack
- backslash
- excape character
- hack character
- '\ (backslash)'
- backslant
- bash
- reverse slant
- slosh
- reversed virgule
- line continuation character
- reverse solidus
ms.assetid: c97fbb20-3d12-4d0b-9b52-62a229bc83c0
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 99586a80cce43c89aa7ce9a76c84e74652d343be
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="backslash-line-continuation-transact-sql"></a>反斜杠 （续行符） (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

`\`长字符串常量、 字符或二进制文件中，分成两个或多个行，以提高可读性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>参数  
 \<字符串的第一个部分 >  
 是字符串的开头部分。  
  
 \<继续字符串部分 >  
 是字符串的后面部分。  
  
## <a name="remarks"></a>注释  
 该命令将字符串的第一部分和后续部分作为一个字符串返回，中间没有反斜杠。  

## <a name="examples"></a>示例  

### <a name="a-splitting-a-character-string"></a>A. 拆分字符串  

下面的示例使用一个反斜杠和回车字符将字符串拆分成两行。  
  
```  
SELECT 'abc\  
def' AS [ColumnResult];  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    

### <a name="b-splitting-a-binary-string"></a>B. 将二进制字符串拆分  

下面的示例使用一个反斜杠和回车二进制字符串拆分为两行。  

```  
SELECT 0xabc\  
def AS [ColumnResult];  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 0xABCDEF
 ```    

## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40;Division&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40; 除法赋值 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  
