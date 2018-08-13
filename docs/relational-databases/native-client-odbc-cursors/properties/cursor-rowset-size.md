---
title: 游标行集大小 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4e812938bdb8f38008f61bd43339dc694564fdf9
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39541627"
---
# <a name="cursor-rowset-size"></a>游标行集大小
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC 游标并不仅限于一次提取一行。 它们可以检索每次调用中的多个行**SQLFetch**或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。 当与客户端/服务器数据库（例如 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]）一起使用时，可以更有效地一次提取多行。 每次提取返回的行数称为行集大小和使用的 SQL_ATTR_ROW_ARRAY_SIZE 指定[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 行集大小大于 1 的游标称为块状游标。  
  
 有两种方法可用于绑定块状游标的结果集列：  
  
-   按列绑定  
  
     每个列绑定到一个变量数组。 每个数组所具有的元素数目等于行集大小。  
  
-   按行绑定  
  
     使用将所有列的数据和指示符保存在一个行中的结构来构建数组。 数组所具有的结构数目等于行集大小。  
  
 使用按列绑定或按行绑定时，每次调用**SQLFetch**或**SQLFetchScroll**中检索的行集中的数据填充绑定的数组。  
  
 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)还可用于从块游标中检索列数据。 因为**SQLGetData**适用一次一行**SQLSetPos**必须调用以设置特定行的行集中作为当前行之前调用**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序提供了一种优化方式使用行集检索整个结果集快速。 若要使用这种优化，请将游标属性设置为其默认值 (只进、 只读的行集大小 = 1) 次**SQLExecDirect**或**SQLExecute**调用。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序设置了默认结果集。 在不需要滚动的情况下将结果传输到客户端时，该优化功能比服务器游标更有效。 执行语句后，请增加行集大小并使用按列绑定或按行绑定。 这可让[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用默认结果集有效地将结果行发送到客户端，而[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序持续提取这些行，从客户端上的网络缓冲区。  
  
## <a name="see-also"></a>请参阅  
 [游标属性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
