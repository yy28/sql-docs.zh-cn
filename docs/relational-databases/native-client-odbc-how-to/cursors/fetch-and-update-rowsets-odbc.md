---
title: "提取和更新行集 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f1125f69fcc05b5af570a9cc89ed1d9ad0263e1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="fetch-and-update-rowsets-odbc"></a>提取和更新行集 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>提取和更新行集  
  
1.  （可选） 调用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)与 SQL_ROW_ARRAY_SIZE 若要更改的行集中的行 (R) 数。  
  
2.  调用[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)获取行集。  
  
3.  如果使用绑定列，则在行集的绑定列缓冲区中现在可以使用数据值和数据长度。  
  
     如果使用未绑定的列，对于每个行调用[SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407)通过 SQL_POSITION 设置光标位置;，然后为每个未绑定列：  
  
    -   调用[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)最后一个绑定的行集列之后，若要获取的数据的一个或多个时间未绑定列。 调用[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)应递增列号的顺序。  
  
    -   多次调用 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 以从 text 或 image 列获取数据。  
  
4.  设置任意执行时数据 text 或 image 列。  
  
5.  调用[SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407)或[SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398)若要设置光标位置，刷新、 更新、 删除或添加行集内的行。  
  
     如果执行时数据 text 或 image 列用于某个更新或添加操作，则处理它们。  
  
6.  （可选） 执行的定位的 UPDATE 或 DELETE 语句，指定游标名称 (可从[SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)) 和同一个连接上使用不同的语句句柄。  
  
## <a name="see-also"></a>另请参阅  
 [使用游标操作指南主题 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
