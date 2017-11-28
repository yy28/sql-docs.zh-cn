---
title: "文本的前缀和后缀 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f702ed5210b5735a0d3dac418f8296ce274a729b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="literal-prefixes-and-suffixes"></a>文本的前缀和后缀
在 SQL 语句中，*文本*是实际数据值的字符表示。 例如，在下面的语句中，ABC、 FFFF 和 10 是文本：  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 对于某些数据类型的文本需要特殊的前缀和后缀。 在前面的示例中，字符文本 (ABC) 要求单引号 （'） 作为前缀和后缀，二进制文本 (FFFF) 需要的字符 0x 作为前缀，整数文本 (10) 并不要求前缀或后缀。  
  
 对于除日期、 时间和时间戳的所有数据类型，可互操作的应用程序应使用在中创建的结果集的 LITERAL_PREFIX 和 LITERAL_SUFFIX 列中返回的值**SQLGetTypeInfo**。 对于日期、 时间、 时间戳，和日期时间间隔文本中，可互操作的应用程序应使用在上一节中讨论的转义序列。
