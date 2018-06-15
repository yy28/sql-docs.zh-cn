---
title: 文本的前缀和后缀 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77ab92444e7d7c72063a1276c21acd5943ae649e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910602"
---
# <a name="literal-prefixes-and-suffixes"></a>文本的前缀和后缀
在 SQL 语句中，*文本*是实际数据值的字符表示。 例如，在下面的语句中，ABC、 FFFF 和 10 是文本：  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 对于某些数据类型的文本需要特殊的前缀和后缀。 在前面的示例中，字符文本 (ABC) 要求单引号 （'） 作为前缀和后缀，二进制文本 (FFFF) 需要的字符 0x 作为前缀，整数文本 (10) 并不要求前缀或后缀。  
  
 对于除日期、 时间和时间戳的所有数据类型，可互操作的应用程序应使用在中创建的结果集的 LITERAL_PREFIX 和 LITERAL_SUFFIX 列中返回的值**SQLGetTypeInfo**。 对于日期、 时间、 时间戳，和日期时间间隔文本中，可互操作的应用程序应使用在上一节中讨论的转义序列。
