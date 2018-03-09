---
title: SQLProcedures | Microsoft Docs
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
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17ced2d525f863a6a24b1f4a7234cdd1312d7201
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程都返回值。 **SQLProcedures**的结果集列 PROCEDURE_TYPE 报表 SQL_PT_FUNCTION。  
  
 **SQLProcedures**是否值已存在，则返回 SQL_SUCCESS *CatalogName、 SchemaName、*或*ProcName*参数。 **SQLFetch**返回 SQL_NO_DATA，在这些参数中使用了无效值。  
  
 **SQLProcedures**可以执行对静态服务器游标。 尝试执行**SQLProcedures**上的可更新的 （动态或键集） 游标，则将返回 SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 **SQLProcedures**返回有关任何名称匹配的过程的信息*ProcName*并可执行当前用户，或为其当前用户已被授予 VIEW DEFINITION 权限。  
  
## <a name="see-also"></a>另请参阅  
 [SQLProcedures 函数](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
