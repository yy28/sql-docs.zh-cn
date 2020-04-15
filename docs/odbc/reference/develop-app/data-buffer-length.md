---
title: 数据缓冲区长度 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4a4e9a739201d74cfc6c4f7c18e64b91e0fabe4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305258"
---
# <a name="data-buffer-length"></a>数据缓冲区长度
应用程序将数据缓冲区的字节长度传递给参数中的驱动程序，称为*BufferLength*或类似名称。 例如，在以下对**SQLBindCol**的调用中，应用程序指定*ValuePtr*缓冲区的长度 **（sizeof（***ValuePtr）：*****  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 驱动程序将始终返回具有输出字符串参数的任何函数的缓冲区长度参数中的字节数，而不是字符数。  
  
 数据缓冲区长度仅适用于输出缓冲区;驱动程序使用它们来避免写入缓冲区的末尾。 但是，驱动程序仅在缓冲区包含可变长度数据（如字符或二进制数据）时检查数据缓冲区长度。 如果缓冲区包含固定长度数据（如整数或日期结构），则驱动程序将忽略数据缓冲区长度，并假定缓冲区足够大以容纳数据;如果缓冲区大小，则驱动程序将忽略数据缓冲区长度，并假定缓冲区足够大，足以保存数据。也就是说，它永远不会截截固定长度的数据。 因此，应用程序为固定长度数据分配足够大的缓冲区非常重要。  
  
 当出现非数据输出字符串的截断（例如为**SQLGetCursorName**返回的游标名称）时，缓冲区长度参数中返回的长度是可能的最大字符长度。  
  
 输入缓冲区不需要数据缓冲区长度，因为驱动程序不写入这些缓冲区。  
  
 本部分包含以下主题。  
  
-   [使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [数据长度、缓冲区长度和截断](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [字符数据和 C 字符串](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
