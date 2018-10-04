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
manager: craigg
ms.openlocfilehash: a54054387a57d59470bae6d982b5ce700362f483
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635385"
---
# <a name="data-buffer-type"></a>数据缓冲区类型
由应用程序指定的缓冲区的 C 数据类型。 使用一个变量，这发生在应用程序将该变量分配。 与一般内存 — 即内存指向 void 类型的指针的 — 应用程序将强制转换为特定类型的内存时将发生这种情况。 该驱动程序将发现两种方法中的使用此类型：  
  
-   **数据缓冲区类型参数。** 用于传输参数值和结果集数据，如通过绑定的缓冲区的缓冲区*TargetValuePtr*中**SQLBindCol**，通常具有关联的类型参数，例如*TargetType*中的参数**SQLBindCol**。 在此参数中，应用程序传递到缓冲区的类型相对应的 C 类型标识符。 例如，在下面的示例调用到**SQLBindCol**，值 SQL_C_TYPE_DATE 指示驱动程序*日期*缓冲区是 SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     有关类型标识符的详细信息，请参阅[ODBC 中的数据类型](../../../odbc/reference/develop-app/data-types-in-odbc.md)部分中的，稍后在本部分中。  
  
-   **预定义的类型。** 指向用来发送和检索选项或属性，例如缓冲区的缓冲区*InfoValuePtr*中的参数**SQLGetInfo**，具有固定的类型取决于指定的选项。 该驱动程序假设数据缓冲区的此类型;它是应用程序的责任分配此类型的缓冲区。 例如，在下面的示例调用到**SQLGetInfo**，驱动程序假定缓冲区是 32 位整数，因为这是 SQL_STRING_FUNCTIONS 选项的要求：  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 该驱动程序使用的 C 数据类型来解释缓冲区中的数据。
