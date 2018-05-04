---
title: 外部联接转义序列 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31d7ea1f4a349e2a0207481cb85ab898548bd98d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="outer-join-escape-sequence"></a>外部联接转义序列
ODBC 用于外部联接的转义序列。 此转义序列的语法如下所示：  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>注释  
 BNF 表示法中的语法，如下所示是：  
  
 *ODBC 外部的联接的转义*:: =  
  
 *ODBC esc 启动器*oj*外部联接 ODBC esc 终止符*  
  
 *外部联接*:: =*表名*[*相关名称*] {左&#124;右&#124;完整}  
  
 外部联接 {*表名*[*相关名称*] &#124; *外部联接*} ON  
  
 *搜索-*  
  
 *条件*  
  
 *相关名称*:: =*用户定义名称*  
  
 *ODBC esc 启动器*:: = {  
  
 *ODBC esc 终止符*:: =}  
  
 若要确定支持此语句中的哪些部分，应用程序调用**SQLGetInfo** SQL_OJ_CAPABILITIES 信息类型。 对于外部联接，*搜索条件*必须包含仅之间指定的联接条件*表名称*。
