---
title: SQLColumnPrivileges |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0deb4c3099807e42bbc0e5f0e3b588481733c7f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217537"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges**是否存在值都返回 SQL_SUCCESS*CatalogName*， *SchemaName*， *TableName*，或*ColumnName*参数。 **SQLFetch**这些参数中使用的值无效时返回 SQL_NO_DATA。  
  
 **SQLColumnPrivileges**可以对静态服务器游标执行。 尝试执行**SQLColumnPrivileges**对可更新的 （动态或键集） 游标将返回 sql_success_with_info 以指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通过接受由两部分名称来支持链接服务器上的表报告信息*CatalogName*参数： *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>请参阅  
 [SQLColumnPrivileges 函数](http://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
