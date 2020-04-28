---
title: 注释（MDX 语法） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ffcb57a48c7d6e265daa786912cfd37f0b43754
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68001525"
---
# <a name="comments-mdx-syntax"></a>注释（MDX 语法）


  注释是程序代码中不执行的文本字符串。 （注释又称为“备注”。） 可以使用注释说明代码，或者暂时禁用正在诊断的部分多维表达式 (MDX) 语句和脚本。 通过使用注释说明代码，可使程序代码在日后更易于维护。 通常使用注释记录程序名称、作者姓名和主要代码更改的日期。 也可以使用注释说明复杂的计算或解释编程方法。  
  
 MDX 中的注释遵循下列指导原则：  
  
-   注释中可以使用所有字母数字字符或符号。  注释中的所有字符都将被忽略。  
  
-   语句或脚本中的注释没有最大长度限制。 一条注释可由一行或多行组成。  
  
 MDX 支持三种类型的注释字符：  
  
 //（双正斜杠）  
 这些注释字符可与要运行的代码在同一行上，也可单独成一行。 从双正斜杠开始到行尾均为注释部分。 对于多行注释，每个注释行的开始都必须出现双正斜杠。 有关详细信息，请参阅[&#41; &#40;MDX&#41;&#40;注释](../mdx/comment-mdx-double-slash.md)。  
  
 --（双连字符）  
 这些注释字符可与要运行的代码在同一行上，也可单独成一行。 从双连字符开始到行尾均为注释部分。 对于多行注释，每个注释行的开始都必须出现双连字符。 有关详细信息，请参阅[--&#40;注释&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)。  
  
 /* ...\*/（正斜杠-星号字符对）  
 这种注释字符可在要运行的代码行中使用，可以单独成行，也可以位于可执行代码中。 从打开的注释对（/\*）到结束注释对（\*/）的所有内容都被视为注释的一部分。 对于多行注释，打开注释字符对（/\*）必须开始注释，并且结束注释字符对（\*/）必须结束注释。 注释的任何行中均不能出现其他注释字符。 有关详细信息，请参阅[/* .。。/ \*（注释）](../mdx/comment-mdx.md)。  
  
## <a name="example"></a>示例  
 以下查询说明上述三种注释的示例：  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 语法元素 (MDX)](../mdx/mdx-syntax-elements-mdx.md)  
  
  
