---
title: SQLPrimaryKeys |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 49f4373e774ef657b6c17ff4f4aef430b5f651ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  表可能具有一列或可用作唯一行标识符的列，而无需 PRIMARY KEY 约束创建的表返回空结果设置为 SQLPrimaryKeys。 ODBC 函数[SQLSpecialColumns](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md)报表行的没有主键的表的标识符候选项。  
  
 SQLPrimaryKeys 是否值已存在，则返回 SQL_SUCCESS *CatalogName*， *SchemaName*，或*TableName*参数。 SQLFetch 返回 SQL_NO_DATA，在这些参数中使用了无效值。  
  
 SQLPrimaryKeys 可以执行对静态服务器游标。 尝试执行的可更新的 （动态或键集） 游标 SQLPrimaryKeys 将返回 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持为链接服务器上的表报表信息由接受的两部分名称*CatalogName*参数： *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 和表值参数  
 如果语句属性 SQL_SOPT_SS_NAME_SCOPE 具有值 SQL_SS_NAME_SCOPE_TABLE_TYPE，而不是 SQL_SS_NAME_SCOPE_TABLE 其默认值，SQLPrimaryKeys 将返回有关主键列的表类型的信息。 SQL_SOPT_SS_NAME_SCOPE 的详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLPrimaryKeys 函数](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
