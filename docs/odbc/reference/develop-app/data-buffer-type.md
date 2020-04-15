---
title: 数据缓冲区类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b98ed2ab0865b98884f6dfa1ff20142540ff314
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305243"
---
# <a name="data-buffer-type"></a>数据缓冲区类型
缓冲区的 C 数据类型由应用程序指定。 使用单个变量时，当应用程序分配变量时，将发生这种情况。 对于泛型内存（即由类型 void 指针指向的内存），当应用程序将内存转换为特定类型时，就会发生这种情况。 驱动程序通过两种方式发现此类型：  
  
-   **数据缓冲区类型参数。** 用于传输参数值和结果集数据的缓冲区（如**SQLBindCol**中与*TargetValuePtr*绑定的缓冲区）通常具有关联的类型参数，如**SQLBindCol**中的*TargetType*参数。 在此参数中，应用程序传递对应于缓冲区类型的 C 类型标识符。 例如，在以下对**SQLBindCol**的调用中，值SQL_C_TYPE_DATE告诉驱动程序*Date*缓冲区是SQL_DATE_STRUCT：  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     有关类型标识符的详细信息，请参阅本节后面的[ODBC 部分中的数据类型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。  
  
-   **预定义类型。** 用于发送和检索选项或属性的缓冲区（如**SQLGetInfo**中*InfoValuePtr*参数指向的缓冲区）具有依赖于指定选项的固定类型。 驱动程序假定数据缓冲区是此类型;因此，驱动程序假定数据缓冲区为此类型。应用程序负责分配此类型的缓冲区。 例如，在以下对**SQLGetInfo**的调用中，驱动程序假定缓冲区是 32 位整数，因为这是SQL_STRING_FUNCTIONS选项要求：  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 驱动程序使用 C 数据类型来解释缓冲区中的数据。
