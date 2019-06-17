---
title: 外部联接转义序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba08d33efca6fa90531f89bd57a307f42f343ebd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63018370"
---
# <a name="outer-join-escape-sequence"></a>外部联接转义序列
ODBC 使用的外部联接转义序列。 此转义序列的语法如下所示：  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>备注  
 BNF 表示法中的语法是按如下所示：  
  
 *ODBC-outer-join-escape* ::=  
  
 *ODBC esc 启动器*oj*外部联接 ODBC esc 终止符*  
  
 *外部联接*:: = *l e-n* [*相关名称*] {左侧&#124;右&#124;完整}  
  
 外部联接 {*l e-n* [*相关名称*] &#124; *外部联接*} ON  
  
 *search-*  
  
 *condition*  
  
 *correlation-name* ::= *user-defined-name*  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 若要确定支持此语句中的哪些部分，应用程序调用**SQLGetInfo** SQL_OJ_CAPABILITIES 信息类型。 用于外部联接*搜索条件*必须包含仅之间指定的联接条件*表名*。
