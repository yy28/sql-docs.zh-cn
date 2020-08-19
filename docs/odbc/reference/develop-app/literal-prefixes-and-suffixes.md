---
description: 文本前缀和后缀
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0f658c401bfc31e69a6e5e2fc5110bc9a809f345
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424609"
---
# <a name="literal-prefixes-and-suffixes"></a>文本前缀和后缀
在 SQL 语句中， *文本* 是实际数据值的字符表示形式。 例如，在下面的语句中，ABC、FFFF 和10是文本：  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 某些数据类型的文字需要特殊的前缀和后缀。 在前面的示例中，字符文本 (ABC) 需要将单引号 ( ") 作为前缀和后缀，二进制文本 (FFFF) 需要字符0x 作为前缀，并且整数文本 (10) 不需要前缀或后缀。  
  
 对于除 "日期"、"时间" 和 "时间戳" 之外的所有数据类型，可互操作应用程序应使用 LITERAL_PREFIX 中返回的值，并 LITERAL_SUFFIX **SQLGetTypeInfo**创建的结果集中的列。 对于日期、时间、时间戳和日期时间间隔文本，可互操作应用程序应使用上一节中讨论的转义序列。
