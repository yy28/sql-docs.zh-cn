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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915565"
---
# <a name="literal-prefixes-and-suffixes"></a>文本前缀和后缀
在 SQL 语句中，*文字*是实际数据值的字符表示形式。 例如，在下面的语句中，ABC、 FFFF 和 10 是文本：  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 对于某些数据类型的文本需要特殊前缀和后缀。 在前面的示例中，字符文本 (ABC) 要求使用单引号 （'） 作为前缀和后缀，二进制文字 (FFFF) 需要的字符 0x 作为前缀，整数文本 (10) 不需要前缀或后缀。  
  
 对于除日期、 时间和时间戳的所有数据类型，可互操作应用程序应使用在中创建的结果集的 LITERAL_PREFIX 和 LITERAL_SUFFIX 列中返回的值**SQLGetTypeInfo**。 对于日期、 时间、 时间戳和日期时间间隔字符串，可互操作应用程序应使用前面部分所述的转义序列。
