---
title: "SQLFreeStmt |Microsoft 文档"
ms.custom: 
ms.date: 11/23/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e84e2d33e2c6c6a56b0f69f95091b99c81593f9e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  通常   
      **SQLFreeStmt**不建议在 ODBC 3.0 及更高版本。 但是如果应用程序需要重用语句你仍应使用**SQLFreeStmt**与**SQL_RESET_PARAMS**和**SQL_UNBIND**选项)。 你还可以使用[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)， [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)， [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)， [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)，和[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)来替换或重复的函数**SQLFreeStmt**和应改为使用它们。  
  
 一般情况下，它会重用比删除它们并分配新的语句更高效。 但是在某些情况下，重复使用的语句，如 SQLFreeStmt 仍必须使用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLFreeStmt 函数](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
