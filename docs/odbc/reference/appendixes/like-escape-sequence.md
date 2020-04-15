---
title: 喜欢转义序列 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 517c21f7b64fa7ceb662af9839a9fed1a1e6eff6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304918"
---
# <a name="like-escape-sequence"></a>LIKE 转义序列
ODBC 使用 LIKE 子句的转义序列。 此转义序列的语法如下：  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>备注  
 在 BNF 符号中，语法如下所示：  
  
 *ODBC 类似转义*：：*  
  
 *ODBC-esc-发端器*逃生'*逃生字符**'ODBC-esc终结器*  
  
 *转义字符*：：**字符*  
  
 *ODBC-esc -发物人*：：*  
  
 *ODBC-esc 终结器*：*|  
  
 要确定驱动程序是否支持 LIKE 转义序列，应用程序可以使用SQL_LIKE_ESCAPE_CLAUSE信息类型调用**SQLGetInfo。**
