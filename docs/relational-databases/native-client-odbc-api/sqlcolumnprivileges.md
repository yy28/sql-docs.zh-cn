---
title: SQLColumn 特权 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e8197e0a9b105ea6236666a82624ecd97a80568
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302598"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumn 特权**返回SQL_SUCCESS*目录名称*、*架构名称*、*表名*或*列名*参数是否存在值。 当在这些参数中使用无效值时 **，SQLFetch**将返回SQL_NO_DATA。  
  
 **SQLColumn 特权**可以在静态服务器游标上执行。 尝试在可提升（动态或键集）游标上执行**SQLColumn 特权**将返回SQL_SUCCESS_WITH_INFO指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序通过接受*目录名称*参数的两部分名称 *（Linked_Server_Name.Catalog_Name*）支持报告链接服务器上的表的信息。  
  
## <a name="see-also"></a>另请参阅  
 [SQLColumn 特权函数](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
