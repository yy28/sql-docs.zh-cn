---
title: 光标行集大小 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f799722bfae35a714e740691e2cdc53e3155063
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302860"
---
# <a name="cursor-rowset-size"></a>游标行集大小
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 游标并不仅限于一次提取一行。 他们可以检索 SQLFetch 或**SQLFetchScroll** [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)每次调用中的多行。 当与客户端/服务器数据库（例如 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]）一起使用时，可以更有效地一次提取多行。 在提取上返回的行数称为行集大小，并使用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)SQL_ATTR_ROW_ARRAY_SIZE指定。  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 行集大小大于 1 的游标称为块状游标。  
  
 有两种方法可用于绑定块状游标的结果集列：  
  
-   按列绑定  
  
     每个列绑定到一个变量数组。 每个数组所具有的元素数目等于行集大小。  
  
-   行绑定  
  
     使用将所有列的数据和指示符保存在一个行中的结构来构建数组。 数组所具有的结构数目等于行集大小。  
  
 当使用按列或行绑定时，对**SQLFetch**或**SQLFetchScroll**的每个调用都使用从检索的行集中检索的数据填充绑定数组。  
  
 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)还可用于从块游标检索列数据。 由于**SQLGetData**一次工作一行，因此在调用**SQLGetData**之前，必须调用**SQLSetPos**将行集中的特定行设置为当前行。  
  
 本机[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端 ODBC 驱动程序提供使用行集快速检索整个结果集的优化。 要使用此优化，在调用**SQLExecDirect**或**SQLExecute**时，将游标属性设置为其默认值（仅转发、只读、行集大小 = 1）。 本机[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端 ODBC 驱动程序设置默认结果集。 在不需要滚动的情况下将结果传输到客户端时，该优化功能比服务器游标更有效。 执行语句后，请增加行集大小并使用按列绑定或按行绑定。 这允许[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用默认结果集有效地将结果行发送到客户端，而[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序会不断从客户端上的网络缓冲区提取行。  
  
## <a name="see-also"></a>另请参阅  
 [游标属性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
