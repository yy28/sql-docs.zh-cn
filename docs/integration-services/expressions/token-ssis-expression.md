---
title: "TOKEN （SSIS 表达式） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9fdd06bf-5bc9-445c-95bf-709e0ca5989b
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ff578d1f2ba584c64e471fa9514c6fa76e581d8e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="token--ssis-expression"></a>TOKEN（SSIS 表达式）
  基于分隔字符串中的标记的指定分隔符以及表示要返回的标记的标记数目，从字符串返回标记（子字符串）。  
  
## <a name="syntax"></a>语法  
  
```  
TOKEN(character_expression, delimiter_string, occurrence)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 包含分隔符分隔的标记的字符串。  
  
 *delimiter_string*  
 包含分隔符字符的字符串。 例如，“; ,”包含三个分隔符字符，即一个分号、一个空白空间和一个逗号。  
  
 *occurrence*  
 指定要返回的标记的有符号或无符号整数。 例如，如果您指定 3 作为此参数的值，则返回字符串中的第三个标记。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>注释  
 此函数将拆分为一组由 < delimiter_string > 中指定的分隔符分隔的标记的 < character_expression > 字符串并返回的第 n 个标记其中 N 是通过指定的令牌匹配项的数目\<匹配项 > 参数。 有关此函数的用法示例，请参阅“示例”部分。  
  
 下面的备注适用于 TOKEN 函数：  
  
-   分隔符字符串可以包含一个或多个分隔符字符。  
  
-   如果值\<匹配项 > 参数高于的字符串中的令牌的总数目，则函数返回 NULL。  
  
-   前导分隔符将被跳过。  
  
-   TOKEN 只可用于 DT_WSTR 数据类型。 如果 *character_expression* 参数是字符串文字或数据类型为 DT_STR 的数据列，则它在 TOKEN 执行操作前将隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。  
  
-   如果 character_expression 为 Null，则 TOKEN 将返回 Null 结果。  
  
-   您可以使用变量和列作为表达式中所有参数的值。  
  
## <a name="expression-examples"></a>表达式示例  
 在下面的示例中，TOKEN 函数返回“a”。 字符串“a little white dog”具有由分隔符“ ”（空格字符）分隔的 4 个标记“a”、“little”、“white”、“dog”。 第二个参数（分隔符字符串）仅指定要将输入字符串拆分为多个标记的一个分隔符，即空格字符。 最后一个参数 1 指定要返回的第一个标记。 在此示例字符串中，第一个标记是“a”。  
  
```  
TOKEN("a little white dog"," ",1)  
```  
  
 在下面的示例中，TOKEN 函数返回“dog”。 此示例中的分隔符字符串包含 5 个分隔符。 输入字符串包含 4 个标记：“a”、“little”、“white”、“dog”。  
  
```  
TOKEN("a:little|white dog","| ,.:",4)  
```  
  
 在下面的示例中，TOKEN 函数返回 ""（空字符串），因为在字符串中有没有 99 个标记。  
  
```  
TOKEN("a little white dog"," ",99)  
```  
  
 在下面的示例中，TOKEN 函数返回整个字符串。 该函数对分隔符的输入字符串进行分析，因为该字符串中没有任何内容，所以它只是将整个字符串作为第一个标记添加。  
  
```  
TOKEN("a little white dog","|",1)  
```  
  
 在下面的示例中，TOKEN 函数返回“a”。 它将忽略所有前导空格字符。  
  
```  
TOKEN("        a little white dog", " ", 1)  
```  
  
 在下面的示例中，TOKEN 函数从日期字符串中返回年份。  
  
```  
TOKEN("2009/01/01", "/"), 1  
```  
  
 在下面的示例中，TOKEN 函数从指定路径中返回文件名。 例如，如果 User::Path 的值为“c:\program files\data\myfile.txt”，则 TOKEN 函数返回“myfile.txt”。 TOKENCOUNT 函数返回 4，TOKEN 函数第 4 个标记“myfile.txt”。  
  
```  
TOKEN(@[User::Path], "\\", TOKENCOUNT(@[User::Path], "\\"))  
```  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;SSIS 表达式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
