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
manager: craigg
ms.openlocfilehash: 57f4fd34cfe3896bb29ed31f02906ce675e4b854
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640496"
---
# <a name="data-buffer-length"></a>数据缓冲区长度
应用程序传递到名为的参数中的驱动程序的数据缓冲区的字节长度*BufferLength*或类似名称。 例如，在下面的示例调用到**SQLBindCol**，应用程序指定的长度*ValuePtr*缓冲区 (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 驱动程序将始终有一个输出的字符串参数的任何函数的缓冲区长度参数中返回字节，不是数字的字符，数。  
  
 数据缓冲区长度所需的输出缓冲区; 仅驱动程序使用它们来避免写入超过缓冲区的末尾。 不过，仅当在缓冲区中包含可变长度数据，如字符或二进制数据时驱动程序将检查数据缓冲区长度。 如果缓冲区包含固定长度的数据，例如，整数或日期的结构，该驱动程序将忽略数据缓冲区长度，并假定缓冲区是足够大以保存数据;也就是说，它永远不会截断固定长度的数据。 它是因此对于应用程序为固定长度的数据分配足够大的缓冲区。  
  
 非数据被截断输出字符串时出现 (例如游标名称返回有关**SQLGetCursorName**)，缓冲区长度参数中返回的长度是可能的最大字符长度。  
  
 因为该驱动程序不会将这些缓冲区写入，则不需要输入缓冲区的数据缓冲区长度。  
  
 本部分包含以下主题。  
  
-   [使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [数据长度、缓冲区长度和截断](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [字符数据和 C 字符串](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
