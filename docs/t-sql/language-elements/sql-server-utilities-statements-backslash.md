---
title: "（反斜杠）(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
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
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 011025d20b6341b9fa43b25f6c14c91a135a6ffa
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-utilities-statements---backslash"></a>SQL Server 实用工具语句反斜杠
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供了命令不[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，但识别**sqlcmd**和**osql**实用程序和[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]代码编辑器。 这些命令可用于提高批处理和脚本的可读性和执行效率。  
  
\ 分成两个或多个行，以提高可读性常量的长字符串。  
  
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
  
 反斜杠不是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 它是识别的命令**sqlcmd**和**osql**实用程序和[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]代码编辑器。  
  
## <a name="examples"></a>示例  
 下面的示例使用反斜杠和回车符将字符串分成两行。  
  
```  
SELECT 'abc\  
def' AS ColumnResult;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40; 除 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40; 划分等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  

