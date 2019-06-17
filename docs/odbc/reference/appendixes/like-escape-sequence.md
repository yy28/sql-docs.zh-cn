---
title: LIKE 转义序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65447904f32b7e0457ed807f18e942b334ddc236
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188800"
---
# <a name="like-escape-sequence"></a>LIKE 转义序列
ODBC LIKE 子句中使用转义序列。 此转义序列的语法如下所示：  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>备注  
 BNF 表示法中的语法是按如下所示：  
  
 *ODBC-like-escape* ::=  
  
 *ODBC esc 启动器*转义*转义符* *ODBC esc 终止符*  
  
 *escape-character* ::= *character*  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 若要确定驱动程序是否支持 LIKE 转义序列，应用程序可以调用**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 信息类型。
