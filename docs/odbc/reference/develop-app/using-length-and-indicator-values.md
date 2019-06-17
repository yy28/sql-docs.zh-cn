---
title: 使用长度和指示器值 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 442d0865ede4819ea3413d662411295daa5b48bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62501108"
---
# <a name="using-length-and-indicator-values"></a>使用长度和指示器值
长度/指示器缓冲区用于传递的数据缓冲区或如 SQL_NULL_DATA，指示数据为 NULL 的特殊指示器中的数据的字节长度。 根据使用它的函数，定义长度/指示器缓冲区为 SQLINTEGER 或 SQLSMALLINT。 因此，单个参数需要对其进行描述。 数据缓冲区是否 nondeferred 输入的缓冲区，则此参数包含数据本身的字节长度或指示器值。 它通常名为*StrLen_or_Ind*或类似名称。 例如，下面的代码调用**SQLPutData**传递缓冲区的数据; 的字节长度 (*ValueLen*) 直接传递，因为数据缓冲区 (*ValuePtr*) 是输入的缓冲区。  
  
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
  
 如果延迟的输入的缓冲区、 nondeferred 的输出缓冲区或输出缓冲区的数据缓冲区，该参数包含长度/指示器缓冲区的地址。 它通常名为*StrLen_or_IndPtr*或类似名称。 例如，下面的代码调用**SQLGetData**若要检索的数据; 完整的缓冲区的字节长度返回到长度/指示器缓冲区中的应用程序 (*ValueLenOrInd*)，其地址是传递给**SQLGetData**因为相应的数据缓冲区 (*ValuePtr*) 是 nondeferred 的输出缓冲区。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非明确禁止，长度/指示器缓冲区参数可以是 0 (如果 nondeferred 的输入) 或 null 指针 (如果输出或延迟的输入)。 对于输入缓冲区，这会导致驱动程序忽略数据的字节长度。 这将传递长度可变的数据时将返回错误，但时很常见传递非 null 的固定长度数据，因为长度和指示器值都不需要。 对于输出缓冲区，这会导致要返回的数据或指示器值的字节长度的驱动程序。 如果驱动程序返回的数据为 NULL，但因为长度和指示器值都不需要为常见检索固定长度，不可以为 null 的数据时，这是一个错误。  
  
 当延迟的数据缓冲区的地址传递给驱动程序，作为延迟的长度/指示器缓冲区的地址必须保持有效，直到取消绑定此缓冲区。  
  
 以下的长度是作为长度/指示器值无效：  
  
-   *n*，其中*n* > 0。  
  
-   0.  
  
-   SQL_NTS. 发送到相应的数据缓冲区中的驱动程序的字符串是以 null 结尾;这是 C 程序员可以传递字符串，而无需计算它们的字节长度的简便方法。 仅当应用程序将数据发送到该驱动程序时，此值是合法的。 当驱动程序将数据返回到应用程序时，它始终返回数据的实际字节长度。  
  
 以下值是作为长度/指示器值无效。 SQL_NULL_DATA 存储在 SQL_DESC_INDICATOR_PTR 描述符字段;所有其他值都存储在 SQL_DESC_OCTET_LENGTH_PTR 描述符字段。  
  
-   SQL_NULL_DATA. 数据为 NULL 数据值，而忽略相应的数据缓冲区中的值。 此值是合法只能用于 SQL 数据发送到或从该驱动程序检索到的。  
  
-   SQL_DATA_AT_EXEC. 数据缓冲区不包含任何数据。 相反，数据将发送具有**SQLPutData**执行该语句时或当**SQLBulkOperations**或**SQLSetPos**调用。 此值是仅对发送到该驱动程序的 SQL 数据合法的。 有关详细信息，请参阅[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，并[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   结果 SQL_LEN_DATA_AT_EXEC (*长度*) 宏。 此值是类似于 SQL_DATA_AT_EXEC。 有关详细信息，请参阅[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 该驱动程序无法确定长数据仍可用于在输出缓冲区中返回的字节数。 此值是只能用于从驱动程序检索到的 SQL 数据合法的。  
  
-   SQL_DEFAULT_PARAM. 一个过程是而不是相应的数据缓冲区中的值的过程中使用输入参数的默认值。  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations**或**SQLSetPos**是忽略数据缓冲区中的值。 通过调用更新数据行时**SQLBulkOperations**或**SQLSetPos，** 列的值不会更改。 通过调用插入新数据行时**SQLBulkOperations**，列的值设置为其默认值; 如果列没有默认值为 NULL。
