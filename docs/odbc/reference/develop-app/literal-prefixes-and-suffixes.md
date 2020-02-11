---
title: 文本前缀和后缀 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 56ee50071f622c114bd6d8d04444e78c0fb69d67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915565"
---
# <a name="literal-prefixes-and-suffixes"></a>文本前缀和后缀
在 SQL 语句中，*文本*是实际数据值的字符表示形式。 例如，在下面的语句中，ABC、FFFF 和10是文本：  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 某些数据类型的文字需要特殊的前缀和后缀。 在前面的示例中，字符文本（ABC）要求使用单引号（'）作为前缀和后缀，二进制文本（FFFF）需要字符0x 作为前缀，整数文本（10）不需要前缀或后缀。  
  
 对于除 "日期"、"时间" 和 "时间戳" 之外的所有数据类型，可互操作应用程序应使用 LITERAL_PREFIX 中返回的值，并 LITERAL_SUFFIX **SQLGetTypeInfo**创建的结果集中的列。 对于日期、时间、时间戳和日期时间间隔文本，可互操作应用程序应使用上一节中讨论的转义序列。
