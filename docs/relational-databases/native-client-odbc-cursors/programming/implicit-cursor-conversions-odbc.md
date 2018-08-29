---
title: 隐式游标转换 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8b04cbd2ee399e2a99b4e0679fb502e227d44fcf
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43065057"
---
# <a name="implicit-cursor-conversions-odbc"></a>隐式游标转换 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  应用程序可以请求通过游标类型[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) ，然后执行请求的类型的服务器游标不支持的 SQL 语句。 调用**SQLExecute**或**SQLExecDirect**返回 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**返回：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 应用程序可以确定的游标类型现在正在使用通过调用**SQLGetStmtOption**设置为 SQL_CURSOR_TYPE。 游标类型转换仅适用于一个语句。 下一步**SQLExecDirect**或**SQLExecute**都使用原始的语句游标设置。  
  
## <a name="see-also"></a>请参阅  
 [游标编程详细信息&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
