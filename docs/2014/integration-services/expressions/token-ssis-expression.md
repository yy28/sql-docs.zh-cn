---
title: TOKEN（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9fdd06bf-5bc9-445c-95bf-709e0ca5989b
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 826eea9ec6160568bf4eb63d5ddf7bf27ca7502d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263204"
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
  
## <a name="remarks"></a>Remarks  
 此函数将 <character_expression> 字符串拆分为一组由 <delimiter_string> 中指定的分隔符分隔的标记，然后返回第 N 个标记，其中 N 是 \<occurrence> 参数指定的标记出现的次数。 有关此函数的用法示例，请参阅“示例”部分。  
  
 下面的备注适用于 TOKEN 函数：  
  
-   分隔符字符串可以包含一个或多个分隔符字符。  
  
-   如果 \<occurrence> 参数的值大于字符串中标记的总数，则该函数返回 NULL。  
  
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
  
## <a name="see-also"></a>请参阅  
 [函数&#40;SSIS 表达式&#41;](functions-ssis-expression.md)  
  
  
