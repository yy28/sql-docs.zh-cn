---
title: 字符数据和 C 字符串 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00daac655f0c435c1ee22239d3d4aafa23065997
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217784"
---
# <a name="character-data-and-c-strings"></a>字符数据和 C 字符串
引用变长字符数据 （如列名称、 动态参数和字符串特性值） 的输入的参数有一个关联的长度参数。 如果在应用程序终止 null 字符，因为是在 C 中典型的字符串，它提供了作为自变量中，是以字节为单位的字符串 （不包括 null 终止符） 的长度或 SQL_NTS （Null-Terminated 字符串）。 非负长度参数指定关联的字符串的实际长度。 长度参数可能为 0 以指定长度为零的字符串，即不同于 NULL 值。 负值 SQL_NTS 指示驱动程序以通过定位 null 终止字符确定字符串的长度。  
  
 当字符数据从驱动程序返回到应用程序时，该驱动程序必须始终为 null-将其终止。 这样，应用程序是否为字符串或字符数组中处理数据的选项。 如果应用程序缓冲区足够大，以返回所有字符数据，驱动程序将其截断为所需的 null 终止字符的字节数小于缓冲区的字节长度、 null 终止，截断的数据，并将其存储在缓冲区。 因此，应用程序始终必须分配额外的空间，用来检索字符数据的缓冲区中的 null 终止字符。 例如，需要 51 字节缓冲区来检索数据的 50 个字符。  
  
 特殊格外小心，必须按应用程序和驱动程序时发送或检索长字符数据中使用部件**SQLPutData**或**SQLGetData**。 如果数据作为一系列以 null 结尾的字符串传递，可以重新组合数据之前必须去除对这些字符串的 null 终止字符。  
  
 字符数据和 C 字符串具有混淆的 ODBC 程序员数。 发生了这是定义 ODBC 函数时使用的 C 语言的项目。 如果 ODBC 驱动程序或应用程序使用另一种语言-请记住，ODBC 是独立于语言的-这种混乱情况很少出现。  
  
 当 C 字符串用于保存字符数据时，null 终止字符不被视为是数据的一部分，并不计作其字节长度的一部分。 例如，可以将字符数据"ABC"保存为"ABC\0"的 C 字符串或字符数组 {A、 B、 C}。 数据的字节长度为 3，指示将其视为字符串或字符数组。  
  
 尽管应用程序和驱动程序通常使用 C 字符串 （以 null 结尾的字符数组） 来存放字符数据，但并不需要执行此操作。 在 C 中，字符数据可以也被视为一个数组 （没有 null 终止） 字符和长度/指示器缓冲区中单独传递其字节长度。  
  
 由于字符数据可以保存在非 null 终止的数组，并且其字节长度单独传递，则可以在字符数据中嵌入的 null 字符。 但是，ODBC 函数的行为在这种情况下未定义，它是特定于驱动程序是否将驱动程序处理此正确。 因此，可互操作应用程序应始终处理字符数据可以包含嵌入的 null 字符作为二进制数据。
