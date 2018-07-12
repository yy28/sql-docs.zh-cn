---
title: 隐式游标转换 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60fabee858409f65a73bb03749a64b532e79d66b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422326"
---
# <a name="implicit-cursor-conversions-odbc"></a>隐式游标转换 (ODBC)
  应用程序可以请求通过游标类型[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) ，然后执行请求的类型的服务器游标不支持的 SQL 语句。 调用**SQLExecute**或**SQLExecDirect**返回 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**返回：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 应用程序可以确定的游标类型现在正在使用通过调用**SQLGetStmtOption**设置为 SQL_CURSOR_TYPE。 游标类型转换仅适用于一个语句。 下一步**SQLExecDirect**或**SQLExecute**都使用原始的语句游标设置。  
  
## <a name="see-also"></a>请参阅  
 [游标编程详细信息&#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
