---
title: 设置 ANSI 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d32e4dc27568b37f273ef654ebd45d26ca23e555
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997766"
---
# <a name="set-ansi-command"></a>SET ANSI 命令
确定不同长度的字符串在 Visual FoxPro SQL 命令中与 = 运算符进行比较的方式。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （驱动程序的默认值; Visual FoxPro 的默认值为 OFF。）将较短的字符串填充为与较长的字符串长度相等所需的空白。 然后，将两个字符串的字符的字符与字符进行比较。 请考虑此比较：  
  
```  
'Tommy' = 'Tom'  
```  
  
 结果为 False （。如果设置 ANSI 为 on，则在填充时，"Tom" 将变为 "Tom" 并且字符串 "Tom" 和 "Tommy" 不匹配字符。  
  
 = = 运算符使用此方法在 Visual FoxPro SQL 命令中进行比较。  
  
 OFF  
 指定不用空格填充较短的字符串。 这两个字符串在达到较短字符串的末尾之前，会对字符进行比较。 请考虑此比较：  
  
```  
'Tommy' = 'Tom'  
```  
  
 结果为 True （。如果设置 ANSI 为 off，则为 off，因为比较在 "Tom" 后停止。  
  
## <a name="remarks"></a>备注  
 设置 ANSI 确定在进行 SQL 字符串比较时，是否用空白填充两个字符串中较短的一个。 SET ANSI 对 = = 运算符不起任何作用;当使用 = = 运算符时，将始终用空白填充较短的字符串进行比较。  
  
## <a name="string-order"></a>字符串顺序  
 在 SQL 命令中，在比较中的两个字符串的从左到右的顺序为 irrelevantswitching 从 = 或 = = 运算符的一侧到另一侧的字符串，而不会影响比较结果。  
  
## <a name="see-also"></a>另请参阅  
 [SELECT-SQL 命令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)
