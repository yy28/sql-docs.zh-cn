---
title: 数据缓冲区类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 615625ca396e5f2ae094962457cc9e746730ddcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067416"
---
# <a name="data-buffer-type"></a>数据缓冲区类型
缓冲区的 C 数据类型由应用程序指定。 使用单个变量时，应用程序分配变量时会出现这种情况。 对于泛型内存（即，类型为 void 的指针所指向的内存），如果应用程序将内存强制转换为特定类型，则会发生这种情况。 驱动程序通过两种方式发现此类型：  
  
-   **数据缓冲区类型参数。** 用于传输参数值和结果集数据的缓冲区（如使用**SQLBindCol**中的*TargetValuePtr*绑定的缓冲区）通常具有关联的类型参数，如**SQLBindCol**中的*TargetType*参数。 在此参数中，应用程序传递对应于缓冲区类型的 C 类型标识符。 例如，在以下对**SQLBindCol**的调用中，值 SQL_C_TYPE_DATE 告知驱动程序*日期*缓冲区是 SQL_DATE_STRUCT：  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     有关类型标识符的详细信息，请参阅本部分后面的 " [ODBC 中的数据类型](../../../odbc/reference/develop-app/data-types-in-odbc.md)" 部分。  
  
-   **预定义的类型。** 用于发送和检索选项或属性（例如**SQLGetInfo**中的*InfoValuePtr*参数指向的缓冲区）的缓冲区具有依赖于指定选项的固定类型。 驱动程序假定数据缓冲区为此类型;应用程序负责分配此类型的缓冲区。 例如，在以下对**SQLGetInfo**的调用中，驱动程序假定缓冲区为32位整数，因为这是 SQL_STRING_FUNCTIONS 选项所需的：  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 驱动程序使用 C 数据类型解释缓冲区中的数据。
