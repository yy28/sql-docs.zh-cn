---
title: 光标行为 |微软文档
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2e3400e52cd0b7574c07a3cf813b4cbca317df2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305453"
---
# <a name="cursor-behaviors"></a>游标行为
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 支持通过指定游标的可滚动性和敏感性来指定其行为的 ISO 选项。 这些行为是通过在调用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)时设置SQL_ATTR_CURSOR_SCROLLABLE和SQL_ATTR_CURSOR_SENSITIVITY选项来指定的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通过请求具有以下特征的服务器游标来实现这些选项。  
  
|游标行为设置|请求的服务器游标的特征|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 和 SQL_SENSITIVE|由键集驱动的游标和基于版本的乐观并发|  
|SQL_SCROLLABLE 和 SQL_INSENSITIVE|静态游标和只读并发|  
|SQL_SCROLLABLE 和 SQL_UNSPECIFIED|静态游标和只读并发|  
|SQL_NONSCROLLABLE 和 SQL_SENSITIVE|只进游标和基于版本的乐观并发|  
|SQL_NONSCROLLABLE 和 SQL_INSENSITIVE|默认结果集（只进，只读）|  
|SQL_NONSCROLLABLE 和 SQL_UNSPECIFIED|默认结果集（只进，只读）|  
  
 基于版本的乐观并发需要基础表中**的时间戳**列。 如果在没有**时间戳**列的表上请求基于版本的乐观并发控制，则服务器将使用基于值的乐观并发。  
  
## <a name="scrollability"></a>可滚动性  
 当SQL_ATTR_CURSOR_SCROLLABLE设置为SQL_SCROLLABLE时，光标支持[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)的*Fetch 方向*参数的所有不同值。 当SQL_ATTR_CURSOR_SCROLLABLE设置为SQL_NONSCROLLABLE时，光标仅支持"*提取方向"* 值SQL_FETCH_NEXT。  
  
## <a name="sensitivity"></a>敏感性  
 将 SQL_ATTR_CURSOR_SENSITIVITY 设置为 SQL_SENSITIVE 时，游标可以反映由当前用户所做的或由其他用户提交的数据修改。 将 SQL_ATTR_CURSOR_SENSITIVITY 设置为 SQL_INSENSITIVE 时，游标不能反映数据修改。  
  
## <a name="see-also"></a>另请参阅  
 [使用光标 （ODBC）](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) [光标属性](properties/cursor-properties.md) 
  
  
