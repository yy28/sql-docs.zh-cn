---
title: SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0bd400221a3e199deb50ac8cb384984dc64bca83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014249"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程都返回值。 **SQLProcedures**为结果集列 PROCEDURE_TYPE 报告。  
  
 **SQLProcedures**是否存在值都返回 SQL_SUCCESS *CatalogName、 SchemaName*或*ProcName*参数。 **SQLFetch**这些参数中使用的值无效时返回 SQL_NO_DATA。  
  
 **SQLProcedures**可以对静态服务器游标执行。 尝试执行**SQLProcedures**对可更新的 （动态或键集） 游标将返回 SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 **SQLProcedures**返回其名称匹配的任何过程有关的信息*ProcName*和可由当前用户，或为其当前用户拥有 VIEW DEFINITION 权限。  
  
## <a name="see-also"></a>请参阅  
 [SQLProcedures 函数](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
