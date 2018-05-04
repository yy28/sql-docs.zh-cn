---
title: 如谓词转义字符 |Microsoft 文档
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
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a5615fc4d38f4b74ffa1805576fe836ad9eb2fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="like-predicate-escape-character"></a>如谓词转义字符
在**如**谓词，百分号 （%） 匹配零个或多个任意字符和下划线 (_) 匹配的任何一个字符。 可匹配使用实际的百分比符号或下划线中**如**谓词，转义符必须出现在之前的百分比符号或下划线。 转义序列，用于定义**如**谓词转义符是：  
  
 **{转义***转义符* **}**  
  
 其中*转义符*是数据源支持的任何字符。  
  
 有关更多信息 LIKE 转义序列，请参阅[如转义序列](../../../odbc/reference/appendixes/like-escape-sequence.md)附录 c: SQL 语法中。  
  
 例如，以下 SQL 语句创建相同的客户的结果集的字符"%AAA"开头的名称。 第一个语句中使用转义序列语法。 第二个语句 Microsoft® access 使用的本机语法，并不是可互操作。 请注意，在每个字符的第二个百分比**如**谓词为匹配零个或多个任意字符的通配符。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 若要确定是否**如**谓词转义字符支持的数据源、 应用程序调用**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 选项。
