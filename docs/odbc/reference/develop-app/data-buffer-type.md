---
title: 数据缓冲区类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7f2f6e48c4fd01106b1ccf4a371d4e522587db1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="data-buffer-type"></a>数据缓冲区类型
应用程序指定的缓冲区的 C 数据类型。 使用单一变量，这发生在应用程序将该变量分配。 泛型内存-即，内存的指针指向 void 类型的-发生这种情况是当应用程序将强制转换为特定类型的内存。 该驱动程序发现此类型的两种方法：  
  
-   **数据缓冲区类型自变量。** 用于传输参数值和结果集数据，如通过绑定缓冲区的缓冲区*TargetValuePtr*中**SQLBindCol**，通常具有关联的类型自变量，如*TargetType*中的参数**SQLBindCol**。 在此参数中，应用程序传递到的缓冲区类型对应的 C 类型标识符。 例如，在下面的示例调用**SQLBindCol**，SQL_C_TYPE_DATE 的值指示的驱动程序*日期*缓冲区是 SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     有关类型标识符的详细信息，请参阅[ODBC 中的数据类型](../../../odbc/reference/develop-app/data-types-in-odbc.md)本部分后面的部分。  
  
-   **预定义的类型。** 指向用来发送和检索选项或属性，例如缓冲区的缓冲区*InfoValuePtr*中的参数**SQLGetInfo**，具有依赖于指定的选项的固定的类型。 驱动程序假定数据缓冲区属于此类型;它由应用程序的负责分配此类型的缓冲区。 例如，在下面的示例调用**SQLGetInfo**，驱动程序假定缓冲区是一个 32 位整数，因为这是 SQL_STRING_FUNCTIONS 选项的要求：  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 该驱动程序使用的 C 数据类型来解释缓冲区中的数据。
