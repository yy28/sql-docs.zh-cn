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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 306632f544f144aa4b21e150543c2d4ca5a37d0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47820025"
---
# <a name="buffers"></a>缓冲区
一个缓冲区就是用于应用程序和驱动程序之间传递数据的应用程序任何的内存部分。 例如，应用程序缓冲区可以关联，或*绑定到*结果集列与**SQLBindCol**。 提取每个行，则将返回这些缓冲区中的每列的数据。 *输入缓冲区*用于将数据传递给驱动程序; 应用程序中*输出缓冲区*用于从驱动程序的数据返回到应用程序。  
  
> [!NOTE]  
>  如果 ODBC 函数返回 SQL_ERROR，该函数的任何输出自变量的内容未定义。  
  
 此讨论的焦点本身是主要与不确定类型的缓冲区。 这些缓冲区的地址作为自变量的类型 SQLPOINTER，如出现*TargetValuePtr*中的参数**SQLBindCol**。 但是，一些讨论，如使用缓冲区，使用的参数的项也适用于参数用于将字符串传递给该驱动程序，如*TableName*中的参数**SQLTables**。  
  
 这些缓冲区通常成对出现。 *数据缓冲区*是用于传递数据本身，而*长度/指示器缓冲区*用于传递的数据缓冲区或特殊值，如 SQL_NULL_DATA，指示数据为 NULL 中数据的长度。 数据缓冲区中的数据长度不同于自身的数据缓冲区的长度。 下图显示的数据缓冲区和长度/指示器缓冲区之间的关系。  
  
 ![数据缓冲区和长度&#47;指示器缓冲区](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 当包含数据缓冲区的长度可变的数据，如字符或二进制数据时，长度/指示器缓冲区是必需的。 如果数据缓冲区包含固定长度的数据，例如，整数或日期的结构，则需要长度/指示器缓冲区只是为了通过指示器值，因为已经知道数据的长度。 如果应用程序使用与固定长度的数据的长度/指示器缓冲区，该驱动程序将忽略在它传递任何长度。  
  
 数据缓冲区和它所包含的数据的长度被以字节为单位，而不是字符。 这一区别并不重要的程序的使用 ANSI 字符串，因为在字符和字节的长度都相同。  
  
 当数据缓冲区表示驱动程序定义的描述符字段，诊断字段或属性时，应用程序应指示到驱动程序管理器中指示的字段或属性的值的函数参数的特性。 应用程序通过将字段或属性设置为以下值之一的任何函数调用中设置的长度参数执行此操作。 （同样适用于检索的字段或属性，该参数指向的值设置函数的参数本身中的异常值的函数。）  
  
-   如果指示的字段或属性的值的函数参数是一个字符串，指向*长度*参数是字符串或 sql_nts; 的长度。  
  
-   如果指示的字段或属性的值的函数参数是指向二进制缓冲区的指针，该应用程序将结果放置于的 SQL_LEN_BINARY_ATTR (*长度*) 中的宏*长度*自变量。 这会在负值*长度*参数。  
  
-   如果指示的字段或属性的值的函数参数是指向字符字符串或二进制字符串以外的值的指针*长度*参数应具有 SQL_IS_POINTER 的值。  
  
-   如果指示的字段或属性的值的函数参数包含固定长度的值，*长度*参数是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_ISI_USMALLINT，根据需要。  
  
 本部分包含以下主题。  
  
-   [延迟的缓冲区](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [使用数据缓冲区](../../../odbc/reference/develop-app/using-data-buffers.md)
