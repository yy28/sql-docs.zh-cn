---
title: 缓冲区 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c49e83e12463665f86f8cc15dc595e6ba2c506f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306282"
---
# <a name="buffers"></a>缓冲区
缓冲区是用于在应用程序和驱动程序之间传递数据的任何应用程序内存片段。 例如，应用程序缓冲区可以与**SQLBindCol**的结果集列关联或*绑定到*结果集列。 提取每个行后，将为这些缓冲区中的每一列返回数据。 *输入缓冲区*用于将数据从应用程序传递到驱动程序;*输出缓冲区*用于将数据从驱动程序返回到应用程序。  
  
> [!NOTE]  
>  如果 ODBC 函数返回 SQL_ERROR，则未定义该函数的任何输出参数的内容。  
  
 此讨论主要涉及不确定类型的缓冲区。 这些缓冲区的地址显示为 SQLPOINTER 类型的参数，如**SQLBindCol**中的*TargetValuePtr*参数。 但是，此处所述的某些项目（如与缓冲区一起使用的参数）也适用于将字符串传递给驱动程序的参数，如**SQLTables**中的*TableName*参数。  
  
 这些缓冲区通常成对出现。 *数据缓冲区*用于传递数据本身，而*长度/指示器缓冲区*用于传递数据缓冲区中的数据长度或特殊值（如 SQL_NULL_DATA），这表示数据为 NULL。 数据缓冲区中的数据长度与数据缓冲区本身的长度不同。 下图显示了数据缓冲区和长度/指示器缓冲区之间的关系。  
  
 ![数据缓冲区和长度&#47;指示器缓冲区](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 只要数据缓冲区包含长度可变的数据（如字符或二进制数据），就需要长度/指示器缓冲区。 如果数据缓冲区包含固定长度的数据（如整数或日期结构），则需要长度/指示器缓冲区才能通过指示器值，因为数据的长度已经已知。 如果应用程序使用长度为固定长度数据的长度/指示器缓冲区，则驱动程序将忽略传入的长度为的任何长度。  
  
 数据缓冲区和它所包含的数据的长度都以字节为单位（而不是字符）来度量。 这种区别对于使用 ANSI 字符串的程序是不重要的，因为长度（以字节为单位）和字符相同。  
  
 当数据缓冲区表示驱动程序定义的描述符字段、诊断字段或属性时，应用程序应向驱动程序管理器指示函数参数的性质，该参数指示该字段或属性的值。 应用程序通过在将字段或属性设置为以下值之一的任何函数调用中设置长度参数来实现此功能。 （对于检索字段或特性值的函数也是如此，但参数指向设置函数的值的值在自变量本身中是例外。）  
  
-   如果表示字段或属性的值的函数参数是指向字符串的指针，则*长度*参数为字符串或 SQL_NTS 的长度。  
  
-   如果用于指示该字段或属性的值的函数参数是指向二进制缓冲区的指针，则该应用程序会将 SQL_LEN_BINARY_ATTR （*长度*）宏的结果置于*length*参数中。 这会将负值置于*length*参数中。  
  
-   如果表示字段或属性的值的函数参数是指向字符串或二进制字符串以外的其他值的指针，则*长度*参数应具有 SQL_IS_POINTER 的值。  
  
-   如果指定字段或属性的值的函数参数包含固定长度值，则相应的*长度*参数 SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT 或 SQL_ISI_USMALLINT。  
  
 本部分包含以下主题。  
  
-   [延迟的缓冲区](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [使用数据缓冲区](../../../odbc/reference/develop-app/using-data-buffers.md)
