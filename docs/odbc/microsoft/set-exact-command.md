---
title: "SET 确切命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c94efa07d23249c9fc3e9d661998419b68f7b624
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="set-exact-command"></a>SET 确切命令
指定用于比较两个不同长度的字符串的规则。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 指定的表达式必须匹配要在等效字符的字符。 比较会忽略在表达式中的任何尾随空格。 有关比较，较短的两个表达式填充右侧空白以匹配长的表达式的长度。  
  
 OFF  
 （默认值。）指定，为等效，表达式必须匹配的字符直到到达右侧表达式的末尾。  
  
## <a name="remarks"></a>注释  
 如果两个字符串长度相同，则完全设置的设置无效。  
  
## <a name="string-comparisons"></a>字符串比较  
 Visual FoxPro 具有测试相等的两个关系运算符。  
  
 = 运算符执行的相同类型的两个值之间的比较。 比较字符、 数字、 日期和逻辑数据适合此运算符。  
  
 但是，当比较使用的字符表达式 = 运算符，结果可能不完全符合预期。 比较字符表达式从左到右直到其中一个表达式不等于另一个，直至的右侧表达式的末尾的字符的字符 = 运算符达到 (SET 确切 OFF)，或之前的两个表达式在结束达到 (确切设置 ON)。  
  
 = = 需要确切比较的字符数据时，可以使用运算符。 如果两个字符表达式进行比较与 = = 运算符，两侧的表达式 = = 运算符必须包含完全相同的字符包括空格将被视为相等。 使用比较字符串时，将忽略完全设置的设置 = =。  
  
 下表显示选择的运算符和完全设置的设置如何影响比较。 （下划线表示的空白区域。）  
  
|比较|= 完全关闭|= 确切 ON|= = 确切 ON 或 OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc"="abc"|匹配|匹配|匹配|  
|"ab"="abc"|没有匹配项|没有匹配项|没有匹配项|  
|"abc"="ab"|匹配|没有匹配项|没有匹配项|  
|"abc"="ab_"|没有匹配项|没有匹配项|没有匹配项|  
|"ab"="ab_"|没有匹配项|匹配|没有匹配项|  
|"ab_"="ab"|匹配|匹配|没有匹配项|  
|""="ab"|没有匹配项|没有匹配项|没有匹配项|  
|"ab"=""|匹配|没有匹配项|没有匹配项|  
|"__" = ""|匹配|匹配|没有匹配项|  
|"" = "___"|没有匹配项|匹配|没有匹配项|  
|TRIM("___") =""|匹配|匹配|匹配|  
|""= TRIM("___")|匹配|匹配|匹配|  
  
## <a name="see-also"></a>另请参阅  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
