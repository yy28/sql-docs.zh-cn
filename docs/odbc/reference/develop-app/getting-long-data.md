---
title: 获取长数据 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da901c22eb26af063397b4af184179ebe5c75924
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298987"
---
# <a name="getting-long-data"></a>获取 Long 数据
DBMS 将*长数据*定义为特定大小的任何字符或二进制数据，例如 255 个字符。 此数据可能足够小，可以存储在单个缓冲区中，例如几千个字符的部件描述。 但是，存储在内存中可能太长，例如长文本文档或位图。 由于此类数据不能存储在单个缓冲区中，因此在提取行中的其他数据后，将从具有**SQLGetData**的部件中的驱动程序中检索这些数据。  
  
> [!NOTE]  
>  应用程序实际上可以使用**SQLGetData**检索任何类型的数据，而不仅仅是长数据，尽管只能分批检索字符和二进制数据。 但是，如果数据足够小，可以容纳单个缓冲区，则通常没有理由使用**SQLGetData**。 将缓冲区绑定到列并让驱动程序返回缓冲区中的数据要容易得多。  
  
 若要从列检索长数据，应用程序首先调用**SQLFetchScroll**或**SQLFetch**移动到行并获取绑定列的数据。 然后，应用程序调用**SQLGetData**。 **SQLGetData**的参数与**SQLBindCol**相同：语句句柄;列号;应用程序变量的 C 数据类型、地址和字节长度;和长度/指示器缓冲区的地址。 这两个函数具有相同的参数，因为它们执行的任务基本相同：它们既向驱动程序描述应用程序变量，又指定应返回该变量中特定列的数据。 主要区别是 **，SQLGetData**是在获取行后调用的（由于此原因有时称为*后期绑定*），并且**SQLGetData**指定的绑定仅在调用期间持续。  
  
 对于单个列 **，SQLGetData**的行像**SQLFetch：** 它检索列的数据，将其转换为应用程序变量的类型，并在该变量中返回它。 它还返回长度/指示器缓冲区中数据的字节长度。 有关**SQLFetch**如何返回数据的详细信息，请参阅[获取一行数据](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 **SQLGetData**在一个重要的方面与**SQLFetch**不同。 如果对同一列连续调用该列多次，则每个调用返回数据的连续部分。 除上次调用外，每个调用返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01004（字符串数据，右截断）;最后一次调用返回SQL_SUCCESS。 这是**SQLGetData**用于检索部分长数据的方式。 当没有更多的数据返回时 **，SQLGetData**会返回SQL_NO_DATA。 应用程序负责将长数据放在一起，这可能意味着将数据部分串联。 每个部件都是 null 终止的;因此，每个部件都为 null 终止。如果串联零件，应用程序必须删除 null 终止字符。 可以为可变长度书签和其他长数据检索零件中的数据。 长度/指示器缓冲区中返回的值按上一次调用中返回的字节数减小，尽管驱动程序通常无法发现可用数据量并返回 SQL_NO_TOTAL字节长度。 例如：  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 使用**SQLGetData**有几个限制。 通常，使用**SQLGetData**访问的列：  
  
-   必须按增加列数的顺序进行访问（因为从数据源读取结果集的列的方式）。 例如，为第 5 列调用**SQLGetData，** 然后为列 4 调用它是一个错误。  
  
-   无法绑定。  
  
-   列号必须高于最后一个绑定列。 例如，如果最后一个绑定列是列 3，则为列 2 调用**SQLGetData**是错误的。 因此，应用程序应确保在选择列表的末尾放置长数据列。  
  
-   如果调用**SQLFetch**或**SQLFetchScroll**来检索多行，则无法使用。 有关详细信息，请参阅[使用块光标](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 某些驱动程序不强制执行这些限制。 可互操作的应用程序应假定它们存在，或者通过使用SQL_GETDATA_EXTENSIONS选项调用**SQLGetInfo**来确定不强制实施哪些限制。  
  
 如果应用程序不需要字符或二进制数据列中的所有数据，则可以在执行语句之前设置SQL_ATTR_MAX_LENGTH语句属性，从而减少基于 DBMS 的驱动程序中的网络流量。 这将限制将返回任何字符或二进制列的数据字节数。 例如，假设一列包含长文本文档。 浏览包含此列的表的应用程序可能必须仅显示每个文档的第一页。 尽管可以在驱动程序中模拟此语句属性，但没有理由执行此操作。 特别是，如果应用程序想要截截字符或二进制数据，它应该使用**SQLBindCol**将小缓冲区绑定到列，并让驱动程序截截数据。
