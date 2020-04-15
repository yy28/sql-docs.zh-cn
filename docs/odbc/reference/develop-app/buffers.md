---
title: 缓冲区 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306282"
---
# <a name="buffers"></a>缓冲区
缓冲区是用于在应用程序和驱动程序之间传递数据的任何应用程序内存。 例如，应用程序缓冲区可以与**SQLBindCol**关联或*绑定到*结果集列。 获取每行时，将返回这些缓冲区中每一列的数据。 *输入缓冲区*用于将数据从应用程序传递到驱动程序;*输出缓冲区*用于将数据从驱动程序返回到应用程序。  
  
> [!NOTE]  
>  如果 ODBC 函数返回SQL_ERROR，则该函数的任何输出参数的内容都是未定义的。  
  
 此讨论主要涉及不确定类型的缓冲区。 这些缓冲区的地址显示为 SQLPOINTER 类型的参数，如**SQLBindCol**中的*TargetValuePtr*参数。 但是，此处讨论的某些项（如用于缓冲区的参数）也适用于用于将字符串传递给驱动程序的参数，如**SQLTable**中的*表名称*参数。  
  
 这些缓冲区通常成对。 *数据缓冲区*用于传递数据本身，而*长度/指示器缓冲区*用于传递数据缓冲区中的数据长度或特殊值（如SQL_NULL_DATA），指示数据为 NULL。 数据缓冲区中的数据长度与数据缓冲区本身的长度不同。 下图显示了数据缓冲区与长度/指示器缓冲区之间的关系。  
  
 ![数据缓冲区和长度&#47;指示器缓冲区](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 每当数据缓冲区包含可变长度数据（如字符或二进制数据）时，都需要长度/指示器缓冲区。 如果数据缓冲区包含固定长度数据（如整数或日期结构），则仅需要长度/指示器缓冲区来传递指标值，因为数据的长度已为人所知。 如果应用程序使用长度/指示器缓冲区与固定长度数据，驱动程序将忽略其中传递的任何长度。  
  
 数据缓冲区及其包含的数据的长度以字节为单位进行测量，而不是以字符为单位。 这种区别对于使用 ANSI 字符串的程序来说并不重要，因为字节和字符的长度是相同的。  
  
 当数据缓冲区表示驱动程序定义的描述符字段、诊断字段或属性时，应用程序应向驱动程序管理器指示指示字段或属性值的函数参数的性质。 应用程序通过在将字段或属性设置为以下值之一的任何函数调用中设置 length 参数来进行此种操作。 （检索字段或属性值的函数也是如此，但参数指向设置函数本身的值除外。  
  
-   如果指示字段或属性值的函数参数是指向字符串的指针，则*长度*参数是字符串的长度或SQL_NTS。  
  
-   如果指示字段或属性值的函数参数是指向二进制缓冲区的指针，则应用程序将在*长度*参数中放置SQL_LEN_BINARY_ATTR（*长度*）宏的结果。 这将在*长度*参数中放置负值。  
  
-   如果指示字段或属性值的函数参数是指向字符串或二进制字符串以外的值的指针，*则长度*参数应具有值SQL_IS_POINTER。  
  
-   如果指示字段或属性值的函数参数包含固定长度值，则*长度*参数将根据需要SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT 或SQL_ISI_USMALLINT。  
  
 本部分包含以下主题。  
  
-   [延迟的缓冲区](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [使用数据缓冲区](../../../odbc/reference/develop-app/using-data-buffers.md)
