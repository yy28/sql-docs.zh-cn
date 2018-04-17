---
title: 获取长整型数据 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff0a11691216d03edc80d5be16c18f428664e7b7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getting-long-data"></a>获取长整型数据
Dbms 定义*长整型数据*作为任何字符或通过某些大小，例如 255 个字符的二进制数据。 此数据可能已经足够小，无法存储在单个缓冲区中，例如有几个千位字符的一部分描述。 但是，它可能太长，无法存储在内存中，如长文本文档或位图。 由于此类数据不能存储在单个缓冲区，可从使用部件中的驱动程序检索**SQLGetData**已提取的行中的其他数据之后。  
  
> [!NOTE]  
>  应用程序实际上可以检索任何类型的数据与**SQLGetData**，而不仅仅是长数据，，尽管可以在部件中检索仅字符和二进制数据。 但是，如果数据不足够小，无法放在单个缓冲区，则通常无需使用**SQLGetData**。 它是可以更轻松地将缓冲区绑定到列，并允许将数据返回到缓冲区中的驱动程序。  
  
 若要从列中检索的长整型数据，应用程序首先调用**SQLFetchScroll**或**SQLFetch**移动到某一行并提取的数据绑定列。 然后，应用程序调用**SQLGetData**。 **SQLGetData**具有相同的参数**SQLBindCol**： 语句句柄; 列号; 应用程序变量; 的 C 数据类型、 地址和字节长度和长度/指示器缓冲区的地址。 这两个函数具有相同的参数，因为它们执行实质上是相同的任务： 它们同时描述该驱动程序的应用程序变量并指定应在该变量返回某个特定列的数据。 主要区别如下**SQLGetData**提取行后调用 (有时称为*后期绑定*出于此原因) 和绑定指定的**SQLGetData**仅在调用期间将持续。  
  
 有关单个列， **SQLGetData**表现得像**SQLFetch**： 它检索的列的数据、 将其转换为应用程序变量的类型和返回该变量中。 它还返回长度/指示器缓冲区中的数据的字节长度。 详细了解如何**SQLFetch**返回的数据，请参阅[提取行数据](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 **SQLGetData**区别**SQLFetch**中一个重要方面。 如果不止一次连续为调用相同的列，每个调用将返回连续部分数据。 除最后一次调用每个调用返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （字符串数据，右截断）;最后一次调用返回 SQL_SUCCESS。 这是如何**SQLGetData**用于检索部分中的长整型数据。 若要返回，没有更多数据时**SQLGetData**返回 SQL_NO_DATA。 应用程序负责将长整型数据集中到一起，这可能意味着串联数据的部分。 每个部分是以 null 结尾的;如果串联部件，应用程序必须删除的 null 终止字符。 检索部分的数据可能会出于可变长度书签以及与其他长整型数据。 返回的值中的每个调用在长度/指示器缓冲区降低在以前的调用中，返回的字节数虽然很常见的驱动程序不能发现可用的数据量并返回 SQL_NO_TOTAL 字节长度。 例如：  
  
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
  
 有几个限制使用**SQLGetData**。 通常情况下，与访问列**SQLGetData**:  
  
-   必须递增 （由于结果集的列从数据源中读取的方法） 的列号的顺序访问。 例如，它是错误调用**SQLGetData**为第 5 列，然后调用它的第四列。  
  
-   不能绑定。  
  
-   必须具有更高版本的列数比最后一绑定列。 例如，如果最后一个绑定的列是第 3 列，则会出错调用**SQLGetData**为列 2。 为此，应用程序应确保在选择列表的末尾处放置长整型数据列。  
  
-   如果不能使用**SQLFetch**或**SQLFetchScroll**调用检索多个行。 有关详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 某些驱动程序不会强制这些限制。 可互操作的应用程序应要么假定它们存在，或者确定哪些限制通过调用不会强制执行**SQLGetInfo** SQL_GETDATA_EXTENSIONS 选项。  
  
 如果应用程序不需要的字符或二进制数据列中的所有数据，它可以通过在执行该语句前设置 SQL_ATTR_MAX_LENGTH 语句属性来减少基于 DBMS 的驱动程序中的网络流量。 这会限制将返回的任何字符或二进制列的数据的字节数。 例如，假设某列包含长文本文档。 浏览包含此列的表的应用程序可能需要显示仅每个文档的第一页。 尽管可以驱动程序中模拟此语句属性，但是没有无需执行此操作。 具体而言，如果应用程序想要截断字符或二进制数据，它应将一个较小缓冲区绑定到的列**SQLBindCol**并允许截断的数据的驱动程序。
