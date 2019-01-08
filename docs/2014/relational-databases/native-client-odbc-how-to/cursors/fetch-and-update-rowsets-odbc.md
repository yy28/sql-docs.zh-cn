---
title: 提取和更新行集 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f04184e968b60a58c4adfa067d516b58b0a43292
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352637"
---
# <a name="fetch-and-update-rowsets-odbc"></a>提取和更新行集 (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>提取和更新行集  
  
1.  （可选） 调用[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)使用 SQL_ROW_ARRAY_SIZE 若要更改的行集中的行 (R) 数。  
  
2.  调用[SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)获取行集。  
  
3.  如果使用绑定列，则在行集的绑定列缓冲区中现在可以使用数据值和数据长度。  
  
     如果使用未绑定的列，为每个行调用[SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407)使用 SQL_POSITION 设置游标位置，然后，为每个未绑定列：  
  
    -   调用[SQLGetData](../../native-client-odbc-api/sqlgetdata.md)最后一个绑定列的行集后，若要获取的数据的一个或多个时间未绑定列。 调用[SQLGetData](../../native-client-odbc-api/sqlgetdata.md)应按列号递增的顺序。  
  
    -   多次调用 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 以从 text 或 image 列获取数据。  
  
4.  设置任意执行时数据 text 或 image 列。  
  
5.  调用[SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407)或[SQLBulkOperations](https://go.microsoft.com/fwlink/?LinkId=58398)若要设置光标位置，刷新、 更新、 删除或添加该行集内的行。  
  
     如果执行时数据 text 或 image 列用于某个更新或添加操作，则处理它们。  
  
6.  （可选） 执行定位的 UPDATE 或 DELETE 语句时，指定游标名称 (可从[SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)) 和同一连接上使用不同的语句句柄。  
  
## <a name="see-also"></a>请参阅  
 [使用游标操作指南主题&#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  
