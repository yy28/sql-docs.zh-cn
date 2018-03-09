---
title: SQLColumnPrivileges | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 862796aba363d2d7811a7e2d557dbf38a9280085
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumnPrivileges**是否值已存在，则返回 SQL_SUCCESS*CatalogName*， *SchemaName*， *TableName*，或*ColumnName*参数。 **SQLFetch**返回 SQL_NO_DATA，在这些参数中使用了无效值。  
  
 **SQLColumnPrivileges**可以执行对静态服务器游标。 尝试执行**SQLColumnPrivileges**上的可更新的 （动态或键集） 游标，则将返回 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持为链接服务器上的表报表信息由接受的两部分名称*CatalogName*参数： *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>另请参阅  
 [SQLColumnPrivileges 函数](http://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
