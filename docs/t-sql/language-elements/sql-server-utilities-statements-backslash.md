---
title: 反斜杠（行继续符）(Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
helpviewer_keywords:
- backwhack
- backslash
- escape character
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 54e1dcd9735610f7cc8f109f00aa56fa7728ce04
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495435"
---
# <a name="backslash-line-continuation-transact-sql"></a>反斜杠（行继续符）(Transact SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

`\` 将一个长字符串常量、字符或二进制分成两行或更多行，以方便阅读。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>参数  
 \<first section of string>  
 是字符串的开头部分。  
  
 \<continued section of string>  
 是字符串的后面部分。  
  
## <a name="remarks"></a>Remarks  
该命令将字符串的第一部分和后续部分作为一个字符串返回，中间没有反斜杠。 反斜杠后的新行必须是换行符 (U + 000A) 或回车符 (U + 000D) 和换行符 (U + 000A) 的组合。 

## <a name="examples"></a>示例  

### <a name="a-splitting-a-character-string"></a>A. 拆分字符串  

以下示例使用反斜杠和回车符将字符串分成两行。  
  
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

### <a name="b-splitting-a-binary-string"></a>B. 拆分二进制字符串  

以下示例使用反斜杠和回车符将二进制字符串分成两行。  

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
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)   
 [(Division) (Transact-SQL)](../../t-sql/language-elements/divide-transact-sql.md)   
 [（除法赋值）(Transact-SQL)](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [复合运算符 (Transact-SQL)](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  
