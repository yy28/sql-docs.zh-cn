---
title: "SET ANSI 命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef87baef7367068b5a22225f3bb9b4c3e1783ca6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="set-ansi-command"></a>SET ANSI 命令
确定如何使用进行的不同长度的字符串之间的比较 = Visual FoxPro SQL 命令中的运算符。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （默认为驱动程序; Visual FoxPro 的默认值为 OFF。）空白使用较短字符串所需的填充使其等于越长字符串的长度。 两个字符串然后比较其整个长度的字符的字符。 请考虑这种比较：  
  
```  
'Tommy' = 'Tom'  
```  
  
 结果为 False (。F.) 如果设置 ANSI 处于打开状态，因为当填充的 Tom 变为 Tom 且字符串 Tom 和 Tommy 不匹配的字符。  
  
 = = 运算符使用此方法用于在 Visual FoxPro SQL 命令中的比较。  
  
 OFF  
 指定用空格不填充较短的字符串。 比较两个字符串字符为字符直到到达较短的字符串的末尾。 请考虑这种比较：  
  
```  
'Tommy' = 'Tom'  
```  
  
 则结果为 True (。T。） 当设置 ANSI 处于关闭状态，因为在 Tom 后停止比较。  
  
## <a name="remarks"></a>Remarks  
 设置 ANSI 确定是否两个字符串的较短者填充空白发出的 SQL 字符串比较。 设置 ANSI 不起任何作用 = = 运算符;当你使用 = = 运算符，使用较短字符串始终填充比较的空白。  
  
## <a name="string-order"></a>字符串顺序  
 在 SQL 命令中比较的两个字符串的从左到右顺序是 irrelevantswitching 字符串中的 = 一侧或 = = 运算符相互不会影响比较的结果。  
  
## <a name="see-also"></a>另请参阅  
 [选择的 SQL 命令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)
