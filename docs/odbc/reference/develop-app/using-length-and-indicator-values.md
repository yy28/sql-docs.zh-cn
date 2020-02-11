---
title: 使用 Length 和指示器值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3a0b54617d55033addabc729adbd078680022fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67902472"
---
# <a name="using-length-and-indicator-values"></a>使用长度和指示器值
长度/指示器缓冲区用于传递数据缓冲区中数据的字节长度或特殊指示器（如 SQL_NULL_DATA），这表示数据为 NULL。 根据使用该函数的函数，长度/指示器缓冲区定义为 SQLINTEGER 或 SQLSMALLINT。 因此，需要使用单个参数来对其进行描述。 如果数据缓冲区是 nondeferred 输入缓冲区，则此参数包含数据本身或指示器值的字节长度。 它通常命名为*StrLen_or_Ind*或类似名称。 例如，下面的代码调用**SQLPutData**以传递缓冲区的全部数据。字节长度（*ValueLen*）是直接传递的，因为数据缓冲区（*将 valueptr*）是一个输入缓冲区。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 如果数据缓冲区是延迟输入缓冲区、nondeferred 输出缓冲区或输出缓冲区，则参数包含长度/指示器缓冲区的地址。 它通常命名为*StrLen_or_IndPtr*或类似名称。 例如，下面的代码调用**SQLGetData**来检索缓冲区的数据;字节长度返回到长度/指示器缓冲区（*ValueLenOrInd*）中的应用程序，其地址传递给**SQLGetData** ，因为相应的数据缓冲区（*将 valueptr*）是 nondeferred 输出缓冲区。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非明确禁止，否则长度/指示器缓冲区参数可以是0（如果为 nondeferred 输入）或 null 指针（如果是输出或延迟输入）。 对于输入缓冲区，这将导致驱动程序忽略数据的字节长度。 这会在传递长度可变的数据时返回错误，但在传递非 null 的固定长度数据时，这会导致错误，因为既不需要长度，也不需要指示器值。 对于输出缓冲区，这将导致驱动程序不返回数据的字节长度或指示器值。 如果驱动程序返回的数据为 NULL，但检索固定长度、不可以为 null 的数据时，这是错误的，因为既不需要长度，也不需要指示器值。  
  
 正如将延迟的数据缓冲区的地址传递给驱动程序一样，延迟长度/指示器缓冲区的地址必须保持有效，直到缓冲区未绑定。  
  
 以下长度作为长度/指示器值有效：  
  
-   *n*，其中*n* > 0。  
  
-   0.  
  
-   SQL_NTS。 发送到相应数据缓冲区中的驱动程序的字符串以 null 结尾;这是一种方便的方法，使 C 程序员无需计算其字节长度即可传递字符串。 仅当应用程序将数据发送到驱动程序时，此值才合法。 当驱动程序将数据返回到应用程序时，它将始终返回数据的实际字节长度。  
  
 以下值作为长度/指示器值有效。 SQL_NULL_DATA 存储在 SQL_DESC_INDICATOR_PTR 描述符字段中;所有其他值都存储在 SQL_DESC_OCTET_LENGTH_PTR 描述符字段中。  
  
-   SQL_NULL_DATA。 数据为 NULL 数据值，并忽略相应数据缓冲区中的值。 此值仅对发送到驱动程序或从驱动程序检索的 SQL 数据是合法的。  
  
-   SQL_DATA_AT_EXEC。 数据缓冲区中不包含任何数据。 相反，当执行语句或调用**SQLBulkOperations**或**SQLSetPos**时，数据将随**SQLPutData**一起发送。 此值仅对发送到驱动程序的 SQL 数据是合法的。 有关详细信息，请参阅[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)和[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   SQL_LEN_DATA_AT_EXEC （*长度*）宏的结果。 此值与 SQL_DATA_AT_EXEC 类似。 有关详细信息，请参阅[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 驱动程序无法确定在输出缓冲区中仍可返回的长数据的字节数。 此值仅对从驱动程序检索的 SQL 数据是合法的。  
  
-   SQL_DEFAULT_PARAM。 过程是在过程中使用输入参数的默认值，而不是对应的数据缓冲区中的值。  
  
-   SQL_COLUMN_IGNORE。 **SQLBulkOperations**或**SQLSetPos**将忽略数据缓冲区中的值。 当通过调用**SQLBulkOperations**或 SQLSetPos 更新行数据时 **，** 列值不会更改。 当通过调用**SQLBulkOperations**插入新的数据行时，列的值设置为其默认值，或者，如果列没有默认值，则设置为 NULL。
