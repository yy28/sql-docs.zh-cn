---
title: "隐式游标转换 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a661774e9be2311a0c7d113356b2fab5a775ba72
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="implicit-cursor-conversions-odbc"></a>隐式游标转换 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  应用程序可以请求通过游标类型[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) ，然后执行请求的类型的服务器游标不支持的 SQL 语句。 调用**SQLExecute**或**SQLExecDirect**返回 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**返回：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 应用程序可以确定哪种类型的游标现在正在使用通过调用**SQLGetStmtOption**设置为 SQL_CURSOR_TYPE。 游标类型转换仅适用于一个语句。 下一步**SQLExecDirect**或**SQLExecute**将完成使用原始的语句游标设置。  
  
## <a name="see-also"></a>另请参阅  
 [光标编程的详细信息 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
