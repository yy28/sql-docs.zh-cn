---
title: SQLColumnPrivileges |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f6afa29c6df3bd0741bd4c2fef1a51478d139420
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35701678"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumnPrivileges**是否值已存在，则返回 SQL_SUCCESS*CatalogName*， *SchemaName*， *TableName*，或*ColumnName*参数。 **SQLFetch**返回 SQL_NO_DATA，在这些参数中使用了无效值。  
  
 **SQLColumnPrivileges**可以执行对静态服务器游标。 尝试执行**SQLColumnPrivileges**上的可更新的 （动态或键集） 游标，则将返回 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持为链接服务器上的表报表信息由接受的两部分名称*CatalogName*参数： *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>请参阅  
 [SQLColumnPrivileges 函数](http://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
