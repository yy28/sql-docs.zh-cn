---
title: LIKE 谓词转义符 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20310c60759aea17d61b9252fd73d226567a7a54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68027228"
---
# <a name="like-predicate-escape-character"></a>LIKE 谓词转义字符
在**LIKE**谓词中，百分号（%）匹配零个或多个任意字符，下划线（_）匹配任何一个字符。 若要匹配**LIKE**谓词中的实际百分比符号或下划线，必须在百分号或下划线前面加上转义符。 定义**LIKE**谓词转义符的转义序列是：  
  
 **{escape \** *转义符* **'}**  
  
 其中， *escape 字符*是数据源支持的任何字符。  
  
 有关类似转义序列的详细信息，请参阅附录 C： SQL 语法中的[转义序列](../../../odbc/reference/appendixes/like-escape-sequence.md)。  
  
 例如，以下 SQL 语句将创建以字符 "% AAA" 开头的客户名称相同的结果集。 第一条语句使用转义序列语法。 第二个语句使用本机语法进行 Microsoft®访问，且不可互操作。 请注意，每个**LIKE**谓词中的第二个百分号字符都是与零个或多个字符匹配的通配符。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 若要确定数据源是否支持**LIKE**谓词转义符，应用程序需要使用 SQL_LIKE_ESCAPE_CLAUSE 选项调用**SQLGetInfo** 。
