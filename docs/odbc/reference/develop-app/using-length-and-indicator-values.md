---
title: 使用长度和指标值 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0c878c9038b26aa996ed206c6b8adfe8d6c21e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306758"
---
# <a name="using-length-and-indicator-values"></a>使用长度和指示器值
长度/指示器缓冲区用于传递数据缓冲区中数据的字节长度或特殊指标（如SQL_NULL_DATA，指示数据为 NULL。 根据使用它的函数，长度/指示器缓冲区定义为 SQLINTEGER 或 SQLSMALLINT。 因此，需要单个参数来描述它。 如果数据缓冲区是非延迟输入缓冲区，则此参数包含数据本身的字节长度或指标值。 它通常命名为*StrLen_or_Ind*或类似的名称。 例如，以下代码调用**SQLPutData**来传递充满数据的缓冲区;字节长度 （*ValueLen*） 直接传递，因为数据缓冲区 （*ValuePtr*） 是输入缓冲区。  
  
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
  
 如果数据缓冲区是延迟输入缓冲区、非延迟输出缓冲区或输出缓冲区，则参数包含长度/指示器缓冲区的地址。 它通常命名为*StrLen_or_IndPtr*或类似的名称。 例如，以下代码调用**SQLGetData**来检索充满数据的缓冲区;字节长度返回到长度/指标缓冲区 *（ValueLenOrInd）* 中的应用程序，其地址传递给**SQLGetData，** 因为相应的数据缓冲区 *（ValuePtr*） 是非延迟输出缓冲区。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非特别禁止，否则长度/指示器缓冲区参数可以是 0（如果未延迟输入）或空指针（如果输出或延迟输入）。 对于输入缓冲区，这将导致驱动程序忽略数据的字节长度。 这在传递可变长度数据时返回错误，但在传递非空固定长度数据时很常见，因为不需要长度或指标值。 对于输出缓冲区，这将导致驱动程序不返回数据的字节长度或指标值。 如果驱动程序返回的数据为 NULL，但在检索固定长度的非空数据时很常见，则这是一个错误，因为不需要长度和指标值。  
  
 当延迟数据缓冲区的地址传递给驱动程序时，延迟长度/指示器缓冲区的地址必须保持有效，直到缓冲区未绑定。  
  
 以下长度作为长度/指示器值有效：  
  
-   *n*，*其中 n* > 0。  
  
-   0.  
  
-   SQL_NTS 发送到相应数据缓冲区中的驱动程序的字符串为 null 终止;因此，发送到驱动程序的字符串为 null，为"已终止"。这是 C 程序员传递字符串而无需计算字节长度的便捷方法。 仅当应用程序将数据发送到驱动程序时，此值才是合法的。 当驱动程序将数据返回给应用程序时，它始终返回数据的实际字节长度。  
  
 以下值作为长度/指示器值有效。 SQL_NULL_DATA存储在SQL_DESC_INDICATOR_PTR描述符字段中;所有其他值都存储在SQL_DESC_OCTET_LENGTH_PTR描述符字段中。  
  
-   SQL_NULL_DATA 数据是 NULL 数据值，并忽略相应数据缓冲区中的值。 此值仅适用于发送到驱动程序或从驱动程序检索的 SQL 数据。  
  
-   SQL_DATA_AT_EXEC 数据缓冲区不包含任何数据。 相反，当执行语句或调用**SQLBulk 操作**或**SQLSetPos**时，数据将随**SQLPutData**一起发送。 此值仅适用于发送到驱动程序的 SQL 数据。 有关详细信息，请参阅[SQLBind参数](../../../odbc/reference/syntax/sqlbindparameter-function.md) [、SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)和[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   SQL_LEN_DATA_AT_EXEC（*长度*）宏的结果。 此值类似于SQL_DATA_AT_EXEC。 有关详细信息，请参阅[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 驱动程序无法确定仍可在输出缓冲区中返回的长数据字节数。 此值仅适用于从驱动程序检索的 SQL 数据。  
  
-   SQL_DEFAULT_PARAM 过程是在过程中使用输入参数的默认值，而不是相应数据缓冲区中的值。  
  
-   SQL_COLUMN_IGNORE。 **SQLBulk 操作**或**SQLSetPos**是忽略数据缓冲区中的值。 通过调用**SQLBulk 操作**或**SQLSetPos**更新一行数据时，列值不会更改。 当通过调用**SQLBulk 操作**插入新数据行时，列值将设置为其默认值，或者如果列没有默认值，则设置为 NULL。
