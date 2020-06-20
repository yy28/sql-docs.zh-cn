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
author: rothja
ms.author: jroth
ms.openlocfilehash: bf46fed47817ed94ea2382f2147df254f2986aec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022753"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges**返回 SQL_SUCCESS*CatalogName*、 *SchemaName*、 *TableName*或*ColumnName*参数是否存在值。 当在这些参数中使用了无效值时， **SQLFetch**将返回 SQL_NO_DATA。  
  
 可以对静态服务器游标执行**SQLColumnPrivileges** 。 尝试对可更新的（动态或键集）游标执行**SQLColumnPrivileges**时，将返回 SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序通过接受由两部分组成的*CatalogName*参数的名称来支持链接服务器上表的报告信息： *Linked_Server_Name。 Catalog_Name*。  
  
## <a name="see-also"></a>另请参阅  
 [SQLColumnPrivileges 函数](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
