---
title: 数据缓冲区长度 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 40fe9d23f14d4a7af80fe31a418cccf7133b7252
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067421"
---
# <a name="data-buffer-length"></a>数据缓冲区长度
应用程序在名为*BufferLength*或类似名称的参数中将数据缓冲区的字节长度传递给驱动程序。 例如，在以下对**SQLBindCol**的调用中，应用程序指定*将 valueptr*缓冲区的长度（**sizeof （***将 valueptr***）**）：  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 对于包含 output string 参数的任何函数，驱动程序将始终返回字节数，而不是字符数。  
  
 数据缓冲区长度仅用于输出缓冲区;驱动程序使用它们来避免写入超过缓冲区的末尾。 但是，仅当缓冲区包含长度可变的数据（如字符或二进制数据）时，驱动程序才会检查数据缓冲区长度。 如果缓冲区包含固定长度的数据（如整数或日期结构），则驱动程序将忽略数据缓冲区长度，并假定缓冲区的大小足以容纳数据;也就是说，它从不截断固定长度数据。 因此，应用程序要为固定长度的数据分配足够大的缓冲区，这一点很重要。  
  
 当发生非数据输出字符串的截断时（例如，为**SQLGetCursorName**返回的游标名称），缓冲区长度参数中返回的长度是可能的最大字符长度。  
  
 对于输入缓冲区，不需要数据缓冲区长度，因为该驱动程序不会写入这些缓冲区。  
  
 本部分包含下列主题。  
  
-   [使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [数据长度、缓冲区长度和截断](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [字符数据和 C 字符串](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
