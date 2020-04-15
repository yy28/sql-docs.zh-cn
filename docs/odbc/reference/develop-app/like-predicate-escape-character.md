---
title: 喜欢谓词转义字符 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e4f04b12911145eede3354532736cb92f1ae413
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306148"
---
# <a name="like-predicate-escape-character"></a>LIKE 谓词转义字符
在**LIKE**谓词中，百分比符号 （%）匹配任何字符的零个或多个，下划线 （*） 匹配任何一个字符。 要匹配**LIKE**谓词中的实际百分比符号或下划线，转义字符必须位于百分比符号或下划线之前。 定义**LIKE**谓词转义字符的转义序列是：  
  
 **[逃生字符***escape-character***]**  
  
 其中*转义字符*是数据源支持的任何字符。  
  
 有关 LIKE 转义序列的详细信息，请参阅附录 C 中的["LIKE 转义序列](../../../odbc/reference/appendixes/like-escape-sequence.md)"：SQL 语法。  
  
 例如，以下 SQL 语句创建以字符"%AAA"开头的客户名称的相同结果集。 第一个语句使用转义序列语法。 第二个语句使用 Microsoft ®访问的原生语法，并且不可互操作。 请注意，每个**LIKE**谓词中的第二个百分比字符是匹配任何字符的零个或多个的通配符。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 要确定数据源是否支持**LIKE**谓词转义字符，应用程序使用SQL_LIKE_ESCAPE_CLAUSE选项调用**SQLGetInfo。**
