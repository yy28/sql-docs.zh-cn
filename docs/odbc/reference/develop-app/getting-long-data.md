---
title: 正在获取长数据 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298987"
---
# <a name="getting-long-data"></a>获取 Long 数据
Dbms 将*长数据*定义为一定大小的任何字符或二进制数据，例如255个字符。 此数据可能足够小，可以存储在单个缓冲区中，例如几个字符的部分说明。 但是，存储在内存中的时间可能太长，例如长文本文档或位图。 由于此类数据不能存储在单个缓冲区中，因此在提取行中的其他数据之后，将从包含**SQLGetData**的部分中的驱动程序检索此类数据。  
  
> [!NOTE]  
>  应用程序可以使用**SQLGetData**（而不只是长数据）检索任何类型的数据，尽管只能在部分中检索字符和二进制数据。 但是，如果数据太小，足以容纳在单个缓冲区中，通常没有理由使用**SQLGetData**。 将缓冲区绑定到列并让驱动程序返回缓冲区中的数据，这要简单得多。  
  
 若要从某一列检索长数据，应用程序首先调用**SQLFetchScroll**或**SQLFetch**移动到某一行，并提取绑定列的数据。 然后，应用程序调用**SQLGetData**。 **SQLGetData**具有与**SQLBindCol**相同的参数：语句句柄;列号;应用程序变量的 C 数据类型、地址和字节长度;和长度/指示器缓冲区的地址。 这两个函数具有相同的参数，因为它们实质上是相同的任务：它们都描述了驱动程序的应用程序变量，并指定应在该变量中返回特定列的数据。 主要区别在于，在提取行之后（出于此原因，有时将其称为*后期绑定*），将调用**SQLGetData** ，并且由**SQLGetData**指定的绑定仅在调用期间持续。  
  
 对于单列， **SQLGetData**的行为类似于**SQLFetch**：它检索列的数据，将其转换为应用程序变量的类型，并将其返回到该变量中。 它还返回长度/指示器缓冲区中数据的字节长度。 有关**SQLFetch**如何返回数据的详细信息，请参阅[提取数据行](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 **SQLGetData**在一个重要方面与**SQLFetch**不同。 如果对同一列连续调用此方法，则每次调用都将返回连续的数据部分。 除最后一个调用之外的每个调用都将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （字符串数据，右端被截断）;最后一个调用返回 SQL_SUCCESS。 这就是使用**SQLGetData**在部分中检索长数据的方式。 当没有更多要返回的数据时， **SQLGetData**将返回 SQL_NO_DATA。 应用程序负责将长数据放在一起，这可能意味着连接数据的各个部分。 每个部件都以 null 结尾;如果连接各个部分，应用程序必须删除 null 终止字符。 对于可变长度书签以及其他长数据，可以在部分中检索数据。 在每次调用时，长度/指示器缓冲区中返回的值会减少上一个调用中返回的字节数，但驱动程序通常不能发现可用数据量并返回 SQL_NO_TOTAL 的字节长度。 例如：  
  
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
  
 使用**SQLGetData**有几个限制。 通常，通过**SQLGetData**访问的列：  
  
-   必须按递增的列号（因为从数据源中读取结果集的列的方式）进行访问。 例如，对第5列调用**SQLGetData**是错误的，然后为第4列调用它。  
  
-   无法绑定。  
  
-   列号必须大于最后一个绑定列的列号。 例如，如果最后一个绑定列是第3列，则为第2列调用**SQLGetData**是错误的。 出于此原因，应用程序应确保将长数据列放在选择列表的末尾。  
  
-   如果调用了**SQLFetch**或**SQLFetchScroll**来检索多个行，则不能使用。 有关详细信息，请参阅[使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 某些驱动程序不会强制实施这些限制。 互操作应用程序应假设它们存在，或通过使用 SQL_GETDATA_EXTENSIONS 选项调用**SQLGetInfo**来确定不强制执行哪些限制。  
  
 如果应用程序不需要字符列或二进制数据列中的所有数据，则可以在执行语句之前设置 SQL_ATTR_MAX_LENGTH 语句特性，从而减少基于 DBMS 的驱动程序中的网络流量。 这会限制将为任何字符列或二进制列返回的数据字节数。 例如，假设某列包含长文本文档。 浏览包含此列的表的应用程序可能必须只显示每个文档的第一页。 尽管可以在驱动程序中模拟此语句属性，但没有必要这样做。 特别是，如果应用程序要截断字符或二进制数据，则应使用**SQLBindCol**将小型缓冲区绑定到该列，并让驱动程序截断数据。
