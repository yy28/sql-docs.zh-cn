---
title: ODBC 游标库 |Microsoft Docs
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
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0ba84589c39298b122bda915fdc01835136e8b1c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555077"
---
# <a name="odbc-cursor-library"></a>ODBC 游标库
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  某些 ODBC 驱动程序仅支持默认游标设置;这些驱动程序也不支持定位的游标操作，如**SQLSetPos**。 ODBC 游标库是用于对通常不支持块状游标或静态游标的驱动程序实现这些游标的 Microsoft 数据访问组件 (MDAC) 的组件。 游标库还实现定位的 UPDATE 和 DELETE 语句和**SQLSetPos**为其创建的游标。  
  
 ODBC 游标库作为 ODBC 驱动程序管理器和 ODBC 驱动程序之间的层实现。 如果加载 ODBC 游标库，ODBC 驱动程序管理器则将与游标相关的所有命令路由到该游标库，而不是驱动程序。 游标库通过从基础驱动程序提取整个结果集并将此结果集缓存到客户端来实现游标。 当使用 ODBC 游标库时，应用程序仅限于该游标库的游标功能；对基础驱动程序中的其他游标功能的支持不可用于该应用程序。  
  
 通常不需要将 ODBC 游标库与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序一起使用，因为与 ODBC 游标库相比，该驱动程序自身支持更多的游标功能。 若要使用 ODBC 游标库使用的唯一原因[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序是因为驱动程序实现其游标支持通过服务器游标，而服务器游标不支持所有 SQL 语句。 如果需要配合使用静态游标和存储过程、批处理或包含 COMPUTE、COMPUTE BY、FOR BROWSE 或 INTO 的 SQL 语句，请考虑使用 ODBC 游标库。 但是，使用游标库时应非常小心，因为它在客户端上缓存整个结果集，这可能占用大量内存并降低性能。  
  
 具有应用程序通过调用游标库基于连接的连接[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)之前连接到数据源设置 SQL_ATTR_ODBC_CURSORS 连接属性。 SQL_ATTR_ODBC_CURSORS 设置为下列三个值之一：  
  
 SQL_CUR_USE_ODBC  
 如果此选项设置使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序，ODBC 游标库则覆盖[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序的本机游标支持。 只有该游标库支持的游标类型才能用于连接；不能使用服务器游标。  
  
 SQL_CUR_USE_DRIVER  
 设置此选项，所有游标支持的本机[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序可以用于连接。 不能使用 ODBC 游标库。 所有游标均作为服务器游标实现。  
  
 SQL_CUR_USE_IF_NEEDED  
 设置此选项，效果时，与使用的 SQL_CUR_USE_DRIVER 相同[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。 在连接时，ODBC 驱动程序管理器进行测试以了解是否连接到的 ODBC 驱动程序支持 SQL_FETCH_PRIOR 选项[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。 如果驱动程序不支持此选项，ODBC 驱动程序管理器则加载 ODBC 游标库。 如果驱动程序支持此选项，ODBC 驱动程序管理器则不加载 ODBC 游标库，应用程序将使用该驱动程序的本机支持。 因为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序支持 SQL_FETCH_PRIOR，ODBC 驱动程序管理器不加载 ODBC 游标库。  
  
 游标库允许应用程序对一个连接使用多个活动语句，以及可滚动、可更新的游标。 必须加载游标库以支持该功能。 使用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)以指定应如何使用游标库和[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)来指定游标类型、 并发和行集大小。  
  
## <a name="see-also"></a>请参阅  
 [如何实现游标](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
