---
title: 设置 ANSI 命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97269642b4147b966fdd71003f5f81ebe7905282
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300907"
---
# <a name="set-ansi-command"></a>SET ANSI 命令
确定如何使用 Visual FoxPro SQL 命令中的 # 运算符对不同长度的字符串进行比较。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （驱动程序的默认值;Visual FoxPro 的默认值为 OFF。用使长度等于较长字符串长度所需的空白填充较短的字符串。 然后，将两个字符串的字符与其整个长度的字符进行比较。 请考虑此比较：  
  
```  
'Tommy' = 'Tom'  
```  
  
 结果是 False （。F.） 如果 SET ANSI 处于打开，因为当填充时，"Tom"变为"汤姆"，字符串"汤姆"和"Tommy"与字符不匹配。  
  
 在 Visual FoxPro SQL 命令中，* 运算符使用此方法进行比较。  
  
 OFF  
 指定较短的字符串不会用空格填充。 在到达较短的字符串之前，将比较字符的两个字符串的字符。 请考虑此比较：  
  
```  
'Tommy' = 'Tom'  
```  
  
 结果为"为"（。T.） 当 SET ANSI 关闭时，因为比较在"Tom"之后停止。  
  
## <a name="remarks"></a>备注  
 SET ANSI 确定在进行 SQL 字符串比较时，是否用空白填充两个字符串的较短时间。 SET ANSI 对 = 运算符没有影响;使用 * 运算符时，较短的字符串始终用空白填充以进行比较。  
  
## <a name="string-order"></a>字符串顺序  
 在 SQL 命令中，比较中两个字符串的从左到右顺序不相关，将字符串从 * 或 * 运算符的一侧切换到另一侧不会影响比较的结果。  
  
## <a name="see-also"></a>另请参阅  
 [选择 - SQL 命令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)
