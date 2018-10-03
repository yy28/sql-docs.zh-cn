---
title: 获取 Long 数据 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d61f6e2d5c2999a1ff7cea86d497eb4f0fb13244
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849435"
---
# <a name="getting-long-data"></a>获取 Long 数据
定义 Dbms*长整型数据*为任何字符或二进制数据而非特定大小，如 255 个字符。 此数据可能很小，可存储在一个缓冲区，例如一部分描述的多个几千个字符。 但是，它可能太长，无法存储在内存中，如长文本文档或位图。 由于此类数据不能存储在一个缓冲区，将从使用部件中的驱动程序中检索**SQLGetData**已提取的行中的其他数据之后。  
  
> [!NOTE]  
>  应用程序可以实际检索任何类型的数据与**SQLGetData**，而不仅仅是长数据，尽管可以在部件中检索仅字符和二进制数据。 但是，如果数据是足够小，无法全部放入一个缓冲区，则通常无需使用**SQLGetData**。 它是更轻松地将缓冲区绑定到的列和让驱动程序在缓冲区中返回数据。  
  
 若要从一列中检索的长整型数据，应用程序首先调用**SQLFetchScroll**或**SQLFetch**移动到某一行并提取对于绑定列的数据。 然后，应用程序调用**SQLGetData**。 **SQLGetData**具有相同的参数**SQLBindCol**： 语句句柄; 列号; 应用程序变量; 的 C 数据类型、 地址和字节长度和长度/指示器缓冲区的地址。 这两个函数具有相同的参数，因为它们执行实质上是相同的任务： 它们都描述向驱动程序应用程序变量，并指定应在该变量中返回的特定列的数据。 主要区别是**SQLGetData**提取行后，将调用 (有时称为*后期绑定*出于此原因)，并且该绑定指定由**SQLGetData**在调用期间持续。  
  
 有关单个列**SQLGetData**的行为类似于**SQLFetch**： 它检索列的数据、 将其转换为应用程序变量的类型并将其返回该变量中。 它还返回长度/指示器缓冲区中的数据的字节长度。 详细了解如何**SQLFetch**返回的数据，请参阅[提取行数据](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 **SQLGetData**不同于**SQLFetch**一个重要方面。 如果调用一次连续的同一列，每个调用将返回连续数据的一部分。 除最后一次调用每个调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （字符串数据，右端被截断）;最后一次调用都返回 SQL_SUCCESS。 这是如何**SQLGetData**用于检索部分中的长整型数据。 若要返回，没有更多数据时**SQLGetData**返回 sql_no_data 为止。 应用程序负责将长数据组合在一起，这可能意味着串联的数据部分。 每个部分是以 null 结尾;如果串联部件，该应用程序必须删除的 null 终止字符。 检索部分中的数据可能会出于长度可变的书签以及与其他长整型数据。 虽然很常见的驱动程序不能发现可用的数据量并返回 SQL_NO_TOTAL 字节长度长度/指示器缓冲区减少在每次调用中返回通过在上一个调用中，返回的字节数的值。 例如：  
  
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
  
 使用的几项限制**SQLGetData**。 通常情况下，与访问列**SQLGetData**:  
  
-   必须按顺序列号递增 （由于从数据源中读取的结果集列的方式） 的访问。 例如，它是错误调用**SQLGetData**为第 5 列，然后调用它的第 4 列。  
  
-   无法绑定。  
  
-   必须具有更高版本的列号比最后一个绑定列。 例如，如果最后一个绑定的列是第 3 列，它是调用错误**SQLGetData**有关第 2 列。 出于此原因，应用程序应确保在选择列表的末尾放置的长整型数据列。  
  
-   如果不能使用**SQLFetch**或**SQLFetchScroll**已调用以检索多个行。 有关详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 某些驱动程序不会强制这些限制。 可互操作应用程序认为它们存在，或确定哪些限制不会通过调用强制执行**SQLGetInfo** SQL_GETDATA_EXTENSIONS 选项。  
  
 如果应用程序不需要的字符或二进制数据列中的所有数据，它可以通过执行语句前设置 SQL_ATTR_MAX_LENGTH 语句属性来减少基于 DBMS 的驱动程序中的网络流量。 这会限制的任何字符或二进制列返回数据的字节数。 例如，假设某个列包含长文本文档。 浏览包含此列的表的应用程序可能需要显示仅每个文档的第一页。 尽管可以在驱动程序中模拟此语句属性，但没有理由要这样做。 具体而言，如果应用程序想要截断字符或二进制数据，它应将较小的缓冲区绑定到的列**SQLBindCol** ，并允许截断的数据的驱动程序。
