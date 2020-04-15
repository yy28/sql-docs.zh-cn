---
title: 提取和更新行集 （ODBC） |微软文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cec50f99fe5f56c9ce613a8b12c0349823f6f461
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299569"
---
# <a name="fetch-and-update-rowsets-odbc"></a>提取和更新行集 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>提取和更新行集  
  
1.  或者，使用SQL_ROW_ARRAY_SIZE调用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)以更改行集中的行数 （R）。  
  
2.  调用[SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)获取行集。  
  
3.  如果使用绑定列，则在行集的绑定列缓冲区中现在可以使用数据值和数据长度。  
  
     如果使用未绑定列，则每行将调用 SQLSetPos，SQL_POSITION设置游标位置;如果使用未绑定列，则调用[SQLSetPos，](https://go.microsoft.com/fwlink/?LinkId=58407)以设置游标位置。然后，对于每个未绑定列：  
  
    -   调用[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)一次或多次，以获取行集最后一个绑定列之后的未绑定列的数据。 对[SQLGetData 的](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)调用应按增加列号的顺序进行。  
  
    -   多次调用 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 以从 text 或 image 列获取数据。  
  
4.  设置任意执行时数据 text 或 image 列。  
  
5.  调用[SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407)或[SQLBulk 操作](https://go.microsoft.com/fwlink/?LinkId=58398)以设置行集中的游标位置、刷新、更新、删除或添加行。  
  
     如果执行时数据 text 或 image 列用于某个更新或添加操作，则处理它们。  
  
6.  或者，执行定位的更新或 DELETE 语句，指定游标名称（可从[SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)中提供），并在同一连接上使用不同的语句句柄。  
  
## <a name="see-also"></a>另请参阅  
 [使用光标操作主题&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
