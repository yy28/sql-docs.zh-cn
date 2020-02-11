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
ms.openlocfilehash: ed99ab72e3d5112588a0b1c93df34b01aff7acdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044917"
---
# <a name="character-data-and-c-strings"></a>字符数据和 C 字符串
引用长度可变的字符数据的输入参数（如列名称、动态参数和字符串属性值）具有关联的长度参数。 如果应用程序使用空字符终止字符串（如 C 中的典型值），则它将以字符串的长度（不包括 null 终止符）或 SQL_NTS （以 Null 结尾的字符串）的形式提供作为参数。 非负长度参数指定关联字符串的实际长度。 长度参数可以为0，以指定长度为零的字符串，该字符串与 NULL 值不同。 负值 SQL_NTS 指示驱动程序通过查找 null 终止字符来确定字符串的长度。  
  
 将字符数据从驱动程序返回到应用程序时，驱动程序必须始终以 null 终止它。 这使应用程序可以选择是否将数据作为字符串或字符数组处理。 如果应用程序缓冲区不够大，无法返回所有字符数据，则驱动程序会将其截断为缓冲区的字节长度，使其不小于 null 终止字符所需的字节数，并将截断后的数据存储在宽限. 因此，应用程序必须始终为用于检索字符数据的缓冲区中的 null 终止字符分配额外的空间。 例如，需要使用51字节缓冲区来检索50个字符的数据。  
  
 在使用**SQLPutData**或**SQLGetData**的部分发送或检索长字符数据时，应用程序和驱动程序必须特别小心。 如果将数据作为以 null 结尾的字符串序列传递，则必须先去除这些字符串的 null 终止字符，然后才能重新组合数据。  
  
 许多 ODBC 程序员都有混淆的字符数据和 C 字符串。 发生这种情况是在定义 ODBC 函数时使用 C 语言的项目。 如果 ODBC 驱动程序或应用程序使用另一种语言-请记住，ODBC 是独立于语言的，这种混乱不太可能发生。  
  
 使用 C 字符串保存字符数据时，不会将 null 终止字符视为数据的一部分，并且不会将其计入字节长度中。 例如，字符数据 "ABC" 可保留为 C 字符串 "ABC\0" 或字符数组 {"A"、"B"、"C"}。 数据的字节长度为3，无论该数据是否被视为字符串或字符数组。  
  
 尽管应用程序和驱动程序通常使用 C 字符串（以 null 结尾的字符数组）来保存字符数据，但不需要执行此操作。 在 C 中，字符数据还可以被视为字符数组（无 null 终止），并在长度/指示器缓冲区中单独传递其字节长度。  
  
 由于字符数据可以保留在非 null 终止的数组中，并且其字节长度是单独传递的，因此可以在字符数据中嵌入空字符。 但是，在这种情况下，ODBC 函数的行为是不确定的，并且它是驱动程序特定的，无论驱动程序是否正确处理。 因此，可互操作的应用程序应始终将可包含嵌入的 null 字符的字符数据作为二进制数据进行处理。
