---
title: "缓冲区 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5953f3409a3886abbf76963d0207a89be1e83aec
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="buffers"></a>缓冲区
缓冲区是用于应用程序和驱动程序之间传递数据的应用程序任何的内存部分。 例如，应用程序缓冲区可以关联，或*绑定到*结果集具有列**SQLBindCol**。 是提取每个行，在这些缓冲区中的每个列返回数据。 *输入缓冲区*用于将数据传递到该驱动程序; 应用程序从*输出缓冲区*用于将数据从驱动程序返回到应用程序。  
  
> [!NOTE]  
>  如果 ODBC 函数返回 SQL_ERROR，任何对该函数的输出自变量的内容是不确定的。  
  
 此讨论的焦点本身主要通过不确定的类型的缓冲区。 这些缓冲区的地址作为自变量的类型 SQLPOINTER，如显示*TargetValuePtr*中的参数**SQLBindCol**。 但是，某些讨论在这里，如使用缓冲区，使用的自变量的项目也适用于自变量用于将字符串传递到该驱动程序，如*TableName*中的参数**SQLTables**。  
  
 这些缓冲区通常成对出现。 *数据缓冲区*是用来传递数据本身，而*长度/指示器缓冲区*用于传递数据缓冲区或如 SQL_NULL_DATA，指示数据为 NULL 的特殊值中的数据的长度。 数据缓冲区中的数据的长度是不同的数据缓冲区本身的长度。 下图显示的数据缓冲区和长度/指示器缓冲区之间的关系。  
  
 ![数据缓冲区和长度 &#47; 指示器缓冲区](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 每当数据缓冲区包含可变长度数据，如字符或二进制数据，长度/指示器缓冲区是必需的。 如果数据缓冲区包含固定长度的数据，如整数或日期结构中，长度/指示器缓冲区只有才需要将传递指示器值，因为已经知道数据的长度。 如果应用程序使用与固定长度的数据的长度/指示器缓冲区，该驱动程序将忽略在它传递任何长度。  
  
 数据缓冲区和它所包含的数据的长度以字节为单位，而不是字符为单位。 这一区别是使用 ANSI 字符串，因为字节数和字符的长度是相同的程序并不重要。  
  
 当数据缓冲区表示驱动程序定义描述符字段、 诊断字段或属性时，应用程序应指示到驱动程序管理器中指示的字段或属性的值的函数参数的性质。 应用程序会通过将长度参数设置为以下值之一设置的字段或属性的所有函数调用中。 （同样适用于检索值的字段或属性，与该参数指向的值设置函数自变量本身中的异常的函数。）  
  
-   如果函数参数指示的字段或属性的值是指向字符串的指针*长度*自变量是字符串或 sql_nts 以的长度。  
  
-   如果函数参数指示的字段或属性的值是指向二进制缓冲区的指针，该应用程序将结果放置于的 SQL_LEN_BINARY_ATTR (*长度*) 中的宏*长度*自变量。 这会在负值*长度*自变量。  
  
-   如果函数参数指示的字段或属性的值是指向字符字符串或二进制字符串以外的值的指针*长度*自变量应具有 SQL_IS_POINTER 的值。  
  
-   如果该函数参数指示的字段或属性的值包含固定长度的值，*长度*自变量是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_ISI_USMALLINT，根据需要。  
  
 本部分包含以下主题。  
  
-   [延迟的缓冲区](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [使用数据缓冲区](../../../odbc/reference/develop-app/using-data-buffers.md)

