---
title: 提取和更新行集（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: rothja
ms.author: jroth
ms.openlocfilehash: 10f23e8a8e8c76160362af2f3efacfd297062254
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018916"
---
# <a name="fetch-and-update-rowsets-odbc"></a>提取和更新行集 (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>提取和更新行集  
  
1.  （可选）通过 SQL_ROW_ARRAY_SIZE 调用[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)来更改行集中的行数（R）。  
  
2.  调用[SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)获取行集。  
  
3.  如果使用绑定列，则在行集的绑定列缓冲区中现在可以使用数据值和数据长度。  
  
     如果使用未绑定的列，则对于每个行调用 SQL_POSITION [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) ，以设置游标位置;然后，对于每个未绑定列：  
  
    -   调用[SQLGetData](../../native-client-odbc-api/sqlgetdata.md)一次或多次，以便在行集的最后一个绑定列后获取未绑定列的数据。 对[SQLGetData](../../native-client-odbc-api/sqlgetdata.md)的调用应按照递增的列号顺序排列。  
  
    -   多次调用 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 以从 text 或 image 列获取数据。  
  
4.  设置任意执行时数据 text 或 image 列。  
  
5.  调用[SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407)或[SQLBulkOperations](https://go.microsoft.com/fwlink/?LinkId=58398)以设置游标位置、刷新、更新、删除或添加行集中的行。  
  
     如果执行时数据 text 或 image 列用于某个更新或添加操作，则处理它们。  
  
6.  （可选）执行定位的 UPDATE 或 DELETE 语句，指定游标名称（可从[SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)获取）并在同一连接上使用不同的语句句柄。  
  
## <a name="see-also"></a>另请参阅  
 [使用游标操作指南主题 &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  
