---
title: LIKE 谓词转义字符 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027228"
---
# <a name="like-predicate-escape-character"></a>LIKE 谓词转义字符
在中**如**谓词，百分号 （%）匹配零个或多个任意字符和下划线 (_) 匹配的任何一个字符。 若要匹配实际的百分比符号或下划线中**如**谓词，转义符必须在之前的百分比符号或下划线。 定义的转义序列**如**谓词转义符是：  
  
 **{转义 '** *转义符* **}**  
  
 其中*转义符*是数据源支持的任何字符。  
  
 详细了解类似转义序列，请参阅[转义序列等](../../../odbc/reference/appendixes/like-escape-sequence.md)附录 c： 驱动器中SQL 语法。  
  
 例如，以下 SQL 语句创建客户相同的结果的集以字符"%AAA"开头的名称。 第一个语句使用转义序列语法。 第二个语句的本机语法用于 Microsoft® 访问并不是可互操作。 请注意，在每个字符的第二个百分比**如**谓词是匹配零个或多个任意字符的通配符字符。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 若要确定是否**等**谓词转义字符支持的数据源、 应用程序调用**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 选项。
