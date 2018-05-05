---
title: 数据缓冲区长度 |Microsoft 文档
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
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b40fb1b58a10ddd5db371869584b4d29f2110855
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="data-buffer-length"></a>数据缓冲区长度
应用程序传递给自变量，名为中的驱动程序的数据缓冲区的字节长度*BufferLength*或类似的名称。 例如，在下面的示例调用**SQLBindCol**，应用程序将指定的长度*ValuePtr*缓冲区 (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 驱动程序将始终有一个输出的字符串参数的任何函数的缓冲区长度参数中返回的字节数不字符数。  
  
 数据缓冲区长度，则只有需要输出缓冲区;驱动程序使用它们来避免写入缓冲区的末尾。 但是，该驱动程序检查数据缓冲区长度，仅在缓冲区包含可变长度数据，如字符或二进制数据时。 如果在缓冲区中包含固定长度的数据，如整数或日期的结构，该驱动程序将忽略数据缓冲区长度，并且假定缓冲区已足够大以保存数据;也就是说，它永远不会截断固定长度的数据。 务必因此应用程序可以为固定长度的数据分配足够大的缓冲区。  
  
 非数据被截断输出字符串时出现 (如游标名称返回**SQLGetCursorName**)，缓冲区长度参数中的返回的长度是可能的最大字符长度。  
  
 因为该驱动程序不会写入这些缓冲区，则不需要输入缓冲区数据缓冲区长度。  
  
 本部分包含以下主题。  
  
-   [使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [数据长度、缓冲区长度和截断](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [字符数据和 C 字符串](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
