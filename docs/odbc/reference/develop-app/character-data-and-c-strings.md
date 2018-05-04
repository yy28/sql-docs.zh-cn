---
title: 字符数据和 C 字符串 |Microsoft 文档
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
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c23f124aeba138e0ffecc432f28fde4c11c7d1b2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="character-data-and-c-strings"></a>字符数据和 C 字符串
引用 （如列名称、 动态参数和字符串特性值） 的长度可变的字符数据的输入的参数具有一个关联的长度参数。 如果在应用程序终止 null 字符，在 C 中的典型的字符串，它提供了作为自变量中，以字节为单位的 （不包括 null 终止符） 的字符串的长度，或者 sql_nts 以 （Null-Terminated 字符串）。 非负长度参数指定的关联字符串的实际长度。 长度参数可能为 0 以指定一个零长度字符串，它是不同于 NULL 值。 负值 sql_nts 以指示要通过定位 null 终止字符确定字符串的长度的驱动程序。  
  
 当字符数据从驱动程序返回到应用程序时，该驱动程序必须始终 null-终止它。 这样，应用程序是否作为字符串或字符数组中处理数据的选择。 如果应用程序缓冲区不足够大，以返回所有字符数据，驱动程序将其截断为更少的所需的 null 终止字符的字节数的缓冲区的字节长度、 null 终止的截断的数据，以及将其存储在缓冲区。 因此，应用程序始终必须为用于检索字符数据的缓冲区中的 null 终止字符分配额外的空间。 例如，若要检索的数据的 50 个字符，需要进行 51 字节缓冲区。  
  
 格外小心，必须通过应用程序和驱动程序发送或检索长时间使用部件中的字符数据时**SQLPutData**或**SQLGetData**。 如果数据作为一系列的以 null 结尾的字符串传递前可以重新合并的数据,，必须剥离这些字符串的 null 终止字符。  
  
 大量的 ODBC 程序员具有混淆字符数据和 C 字符串。 发生这种情况是当定义 ODBC 函数时使用的 C 语言的项目。 如果 ODBC 驱动程序或应用程序使用另一种语言，请记住 ODBC 是独立于语言的 — 这种混乱情况很少会发生。  
  
 当 C 字符串用于保存字符数据时，null 终止字符不被视为可数据的一部分，并且不计数作为其字节长度的一部分。 例如，可以作为 C 字符串"ABC\0"或字符数组 {A、 B、 C} 保留字符数据"ABC"。 数据的字节长度为 3，无论它将被视为字符串或字符数组。  
  
 尽管应用程序和驱动程序通常使用 C 字符串 （以 null 结尾的字符数组） 来保存字符数据，但是没有无需执行此操作。 在 C 中，字符数据可以也被视为字符 （不带 null 终止） 的数组和长度/指示器缓冲区中单独传递其字节长度。  
  
 因为非 – null 结尾的数组中可容纳字符数据，而且其字节长度单独传递，则可以在字符数据中嵌入的空字符。 但是，ODBC 函数的行为在这种情况下是不确定，并且它是特定于驱动程序是否驱动程序处理这种情况正确。 因此，可互操作的应用程序应始终处理可以包含嵌入的 null 字符作为二进制数据的字符数据。
