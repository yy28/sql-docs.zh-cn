---
title: "使用长度和指示器值 |Microsoft 文档"
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
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f615aa92da79c391e84539fdf5cf402d523ab690
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-length-and-indicator-values"></a>使用长度和指示器值
长度/指示器缓冲区用于传递的字节长度的数据缓冲区或如 SQL_NULL_DATA，指示数据为 NULL 的特殊指示器中的数据。 根据使用它的函数，定义长度/指示器缓冲区为 SQLINTEGER 或 SQLSMALLINT。 因此，单个自变量需要对其进行描述。 数据缓冲区是否 nondeferred 输入的缓冲区，该参数将包含的字节长度的数据本身或指示器值。 通常名为*StrLen_or_Ind*或类似的名称。 例如，下面的代码调用**SQLPutData**传递缓冲区的数据的完整; 字节长度 (*ValueLen*) 被直接传递，因为数据缓冲区 (*ValuePtr*) 是输入的缓冲区。  
  
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
  
 如果延迟的输入的缓冲区、 nondeferred 的输出缓冲区或输出缓冲区，数据缓冲区，该参数将包含长度/指示器缓冲区的地址。 通常名为*StrLen_or_IndPtr*或类似的名称。 例如，下面的代码调用**SQLGetData**检索完整的数据; 缓冲区的字节长度就会归还长度/指示器缓冲区中的应用程序 (*ValueLenOrInd*)，其地址是传递给**SQLGetData**因为相应的数据缓冲区 (*ValuePtr*) 是一个 nondeferred 的输出缓冲区。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非专门禁止，长度/指示器缓冲区自变量可以是 0 (如果 nondeferred 的输入) 或 null 指针 (如果输出或延迟的输入)。 对于输入缓冲区，这会导致要忽略的数据的字节长度的驱动程序。 这将传递可变长度数据时将返回错误，但时很常见传递非 null、 固定长度的数据，因为长度和指示器值都不需要。 对于输出缓冲区，这会导致要返回的字节长度的数据或指示器值的驱动程序。 如果驱动程序返回的数据为 NULL，但因为长度和指示器值都不需要是常见检索固定长度、 不可为 null 数据时，这是错误。  
  
 当延迟的数据缓冲区的地址传递到该驱动程序时，延迟的长度指示器缓冲区的地址必须之前一直保持同样有效缓冲区是未绑定。  
  
 以下的长度，则作为长度/指示器值无效：  
  
-   *n*其中 *n*  > 0。  
  
-   0.  
  
-   SQL_NTS 以。 发送到相应的数据缓冲区中的驱动程序的字符串是以 null 结尾的;这是 C 程序员可以传递字符串，而无需计算它们的字节长度的一种简便方式。 仅当应用程序将数据发送到该驱动程序时，此值是合法的。 当该驱动程序将数据返回给应用程序时，它始终返回数据的实际字节的长度。  
  
 以下为有效值为长度/指示器值。 SQL_NULL_DATA 存储在 SQL_DESC_INDICATOR_PTR 描述符字段;所有其他值存储在 SQL_DESC_OCTET_LENGTH_PTR 描述符字段中。  
  
-   SQL_NULL_DATA。 数据为 NULL 数据值，并将忽略相应的数据缓冲区中的值。 此值是合法只能用于 SQL 数据发送到数据库中或从驱动程序检索的。  
  
-   SQL_DATA_AT_EXEC。 数据缓冲区不包含任何数据。 相反，数据将被发送与**SQLPutData**执行语句时或当**SQLBulkOperations**或**SQLSetPos**调用。 此值是合法只能用于 SQL 数据发送到该驱动程序。 有关详细信息，请参阅[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，和[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   结果 SQL_LEN_DATA_AT_EXEC (*长度*) 宏。 此值等同于 SQL_DATA_AT_EXEC。 有关详细信息，请参阅[发送长整型数据](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 该驱动程序无法确定的长整型数据仍可用于返回中输出缓冲区的字节数。 此值是只能用于检索与驱动程序中的 SQL 数据合法的。  
  
-   SQL_DEFAULT_PARAM。 一个过程是而不是相应的数据缓冲区中的值的过程中使用输入参数的默认值。  
  
-   SQL_COLUMN_IGNORE。 **SQLBulkOperations**或**SQLSetPos**是忽略数据缓冲区中的值。 通过调用更新数据行时**SQLBulkOperations**或**SQLSetPos，**列值不会更改。 通过调用插入新的数据行时**SQLBulkOperations**，该列的值设置为其默认值或者，如果列不具有默认情况下，为 NULL。

