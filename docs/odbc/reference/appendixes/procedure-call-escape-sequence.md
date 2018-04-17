---
title: 过程调用转义序列 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5cccd4828a7c7509a3876ac2b194ffccfc6a083d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="procedure-call-escape-sequence"></a>过程调用转义序列
ODBC 使用过程调用中的转义序列。 此转义序列的语法如下所示：  
  
 **{**[？ =]**调用***过程名称*[**(**[*参数*] [，[*参数*]]...**)**]**}**  
  
 BNF 表示法中的语法，如下所示是：  
  
 *ODBC 过程转义*:: =  
  
 &#124;*ODBC esc 启动器*[？ =] 调用*过程 ODBC esc 终止符*  
  
 *过程*:: =*过程名称* &#124; *过程名称*(*过程参数列表*)  
  
 *过程标识符*:: =*用户定义名称*  
  
 *过程名称*:: =*过程标识符*  
  
 &#124;*所有者名称*。*过程标识符*  
  
 &#124;*目录名称的目录分隔符**过程标识符*  
  
 &#124;*目录名称的目录分隔符*[*所有者名称*]。*过程标识符*  
  
 （第三个语法是数据源不支持所有者才有效。）  
  
 *所有者名称*:: =*用户定义名称*  
  
 *目录名称*:: =*用户定义名称*  
  
 *目录分隔符*:: = {*实现定义*}  
  
 (通过返回的目录分隔符**SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 信息选项。)  
  
 *过程参数列表*:: =*过程参数*  
  
 &#124;*过程参数*，*过程参数列表*  
  
 *过程参数*:: =*动态参数* &#124; *文本* &#124; *空字符串*  
  
 *空字符串*:: =  
  
 *ODBC esc 启动器*:: = {  
  
 *ODBC esc 终止符*:: =}  
  
 （如果过程参数是空字符串，该过程使用默认值为该参数。）  
  
 若要确定是否数据源支持过程的驱动程序支持 ODBC 过程调用语法，应用程序可以调用**SQLGetInfo** SQL_PROCEDURES 信息类型。
