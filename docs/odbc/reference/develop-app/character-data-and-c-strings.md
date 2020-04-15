---
title: 字符数据和 C 字符串 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7bb25022d4e0c0559f2a8f77b89a4ba26aeba33a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307487"
---
# <a name="character-data-and-c-strings"></a>字符数据和 C 字符串
引用可变长度字符数据的输入参数（如列名、动态参数和字符串属性值）具有关联的长度参数。 如果应用程序终止带有 null 字符的字符串（如 C 中的典型形式），它将提供字符串的长度（不包括空终止符）或SQL_NTS（空端字符串）。 非负长度参数指定关联字符串的实际长度。 长度参数可以是 0 来指定零长度字符串，该字符串与 NULL 值不同。 负值SQL_NTS通过定位空终止字符指示驱动程序确定字符串的长度。  
  
 当字符数据从驱动程序返回到应用程序时，驱动程序必须始终为 null 终止。 这使应用程序可以选择是将数据作为字符串还是字符数组处理。 如果应用程序缓冲区不够大，无法返回所有字符数据，驱动程序将其截断到缓冲区的字节长度，减去 null 终止字符所需的字节数，null 终止截断的数据，并将其存储在缓冲区中。 因此，应用程序必须始终为用于检索字符数据的缓冲区中的空终止字符分配额外的空间。 例如，需要 51 字节缓冲区来检索 50 个字符的数据。  
  
 在使用**SQLPutData**或**SQLGetData**以部件发送或检索长字符数据时，应用程序和驱动程序必须特别注意。 如果数据作为一系列 null 终止字符串传递，则必须剥离这些字符串上的 null 终止字符，然后才能重新组合数据。  
  
 许多 ODBC 程序员混淆了字符数据和 C 字符串。 发生这种情况是在定义 ODBC 函数时使用 C 语言的一个工件。 如果 ODBC 驱动程序或应用程序使用另一种语言 （ 请记住 ODBC 与语言无关 ） - 这种混淆不太可能发生。  
  
 当 C 字符串用于保存字符数据时，空终止字符不被视为数据的一部分，也不将其计为其字节长度的一部分。 例如，字符数据"ABC"可以作为 C 字符串"ABC_0"或字符数组 ['A'、"B"、"C"*进行维护。 数据的字节长度为 3，无论它被视为字符串还是字符数组。  
  
 尽管应用程序和驱动程序通常使用 C 字符串（空终止字符数组）来保存字符数据，但不需要执行此操作。 在 C 中，字符数据也可以被视为字符数组（不作空终止），其字节长度在长度/指示器缓冲区中单独传递。  
  
 由于字符数据可以位于非 null 端接数组中，并且其字节长度单独传递，因此可以在字符数据中嵌入空字符。 但是，在这种情况下，ODBC 函数的行为是未定义的，并且驱动程序是否正确处理此操作是特定于驱动程序的。 因此，可互操作的应用程序应始终处理可以包含嵌入的空字符作为二进制数据的字符数据。
