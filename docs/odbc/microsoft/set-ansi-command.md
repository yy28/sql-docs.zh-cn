---
title: SET ANSI 命令 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5af98bd8f16d7278b932ad89f1c81c58ddb1fb54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127866"
---
# <a name="set-ansi-command"></a>SET ANSI 命令
确定如何比较不同长度的字符串都是使用 = Visual FoxPro SQL 命令中的运算符。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （默认为驱动程序，Visual FoxPro 的默认值为 OFF。）使用空白较短的字符串所需的面板使其等于越长字符串的长度。 两个字符串随后对其整个长度的字符的比较的字符。 请考虑这种比较：  
  
```  
'Tommy' = 'Tom'  
```  
  
 结果为 False (。F.) 如果将 ANSI 处于打开状态，因为时，Tom 变为 Tom 和 Tom 和 Tommy 的字符串不匹配的字符。  
  
 = = 运算符使用此方法在 Visual FoxPro SQL 命令中的比较。  
  
 OFF  
 指定用空格不填充较短的字符串。 比较两个字符串字符直至达到较短的字符串末尾的字符。 请考虑这种比较：  
  
```  
'Tommy' = 'Tom'  
```  
  
 结果为 True (。T。） 当设置 ANSI 处于关闭状态，因为 Tom 之后停止比较。  
  
## <a name="remarks"></a>备注  
 设置 ANSI 确定是否较短的两个字符串用空格填充时所做的 SQL 字符串比较。 设置 ANSI 不起任何作用 = = 运算符;当你使用 = = 运算符，用来比较的空格始终填充较短的字符串。  
  
## <a name="string-order"></a>字符串顺序  
 SQL 命令中的两个字符串在比较中从左到右顺序是 irrelevantswitching 字符串从一端 = 或 = = 与其他运算符不会影响比较的结果。  
  
## <a name="see-also"></a>请参阅  
 [SELECT-SQL 命令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)
