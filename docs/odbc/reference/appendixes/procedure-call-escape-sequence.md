---
title: 过程调用转义序列 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1194efe6a21c456a722ccd4352661c998f0316d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298217"
---
# <a name="procedure-call-escape-sequence"></a>过程调用转义序列
ODBC 使用转义序列进行过程调用。 此转义序列的语法如下：  
  
 **[**？ ]**调用***过程名称*[**[***参数*] ， **参数** ...**)**]**}**  
  
 在 BNF 符号中，语法如下所示：  
  
 *ODBC-程序转义*：：*  
  
 &#124; *ODBC-esc -发款器*[？ ] 调用*程序 ODBC-esc 终止器*  
  
 *过程*：：**过程名称*&#124;*过程名称*（*过程参数列表*）  
  
 *过程标识符*：：**用户定义的名称*  
  
 *过程名称*：：**过程标识符*  
  
 &#124;*所有者名称*。*过程标识符*  
  
 &#124;*目录名称目录分隔符**过程标识符*  
  
 &#124;*目录名称目录分隔符*=*所有者名称*[所有者名称]。*过程标识符*  
  
 （仅当数据源不支持所有者时，第三个语法才有效。  
  
 *所有者名称*：：**用户定义名称*  
  
 *目录名称*：：**用户定义名称*  
  
 *目录分离器*：：* =*实现定义*|  
  
 （目录分隔符通过**SQLGetInfo**返回，并带有SQL_CATALOG_NAME_SEPARATOR信息选项。  
  
 *过程参数列表*：：**过程参数*  
  
 &#124;*过程参数*，*过程参数列表*  
  
 *过程参数*：：**动态参数*&#124;*文本*&#124;*空字符串*  
  
 *空字符串*：：*  
  
 *ODBC-esc -发物人*：：*  
  
 *ODBC-esc 终结器*：*|  
  
 （如果过程参数为空字符串，则该过程使用该参数的默认值。  
  
 要确定数据源是否支持过程，驱动程序是否支持 ODBC 过程调用语法，应用程序可以使用SQL_PROCEDURES信息类型调用**SQLGetInfo。**
