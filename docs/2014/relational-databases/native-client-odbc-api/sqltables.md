---
title: SQLTables |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLTables function
ms.assetid: 77b6c15c-9cf7-4019-b3f0-3d27d23ef656
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8209bf586e5a0b288b4975869ee8903a73a27f06
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357403"
---
# <a name="sqltables"></a>SQLTables
  SQLTables 可以对静态服务器游标执行。 尝试对可更新的 （动态或键集） 游标执行 SQLTables 将返回 sql_success_with_info 以指示游标类型已更改。  
  
 SQLTables 报告来自所有表数据库何时*CatalogName*参数为 SQL_ALL_CATALOGS 并且所有其他参数包含默认值 （NULL 指针）。  
  
 若要报告可用目录、 架构和表类型，SQLTables 能够特殊使用空字符串 （长度为零字节的指针）。 空字符串不是默认值（NULL 指针）。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通过接受由两部分名称来支持链接服务器上的表报告信息*CatalogName*参数：*Linked_Server_Name.Catalog_Name*。  
  
 SQLTables 返回任何信息的表的名称匹配*TableName*和当前用户所拥有的。  
  
## <a name="sqltables-and-table-valued-parameters"></a>SQLTables 和表值参数  
 如果语句属性 SQL_SOPT_SS_NAME_SCOPE 具有值 SQL_SS_NAME_SCOPE_TABLE_TYPE，而不是其默认值 SQL_SS_NAME_SCOPE_TABLE，SQLTables 返回有关表类型的信息。 SQLTables 返回的结果集的第 4 列中为表类型返回的 TABLE_TYPE 值是表类型。 有关 SQL_SOPT_SS_NAME_SCOPE 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 表、视图和同义词共享公用的命名空间，该命名空间不同于表类型使用的命名空间。 虽然表和视图不能具有相同的名称，但是在相同目录和架构中的表和表类型可以具有相同的名称。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="example"></a>示例  
  
```  
// Get a list of all tables in the current database.  
SQLTables(hstmt, NULL, 0, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of all tables in all databases.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of databases on the current connection's server.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, (SQLCHAR*)"", 0, (SQLCHAR*)"",  
    0, NULL, 0);  
```  
  
## <a name="see-also"></a>请参阅  
 [SQLTables 函数](https://go.microsoft.com/fwlink/?LinkId=59374)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
