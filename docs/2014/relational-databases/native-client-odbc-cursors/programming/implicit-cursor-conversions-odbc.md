---
title: 隐式游标转换（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 99395f9a8dbcb812f5a7764634d42489526875af
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705615"
---
# <a name="implicit-cursor-conversions-odbc"></a>隐式游标转换 (ODBC)
  应用程序可以通过[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)请求游标类型，然后执行所请求类型的服务器游标不支持的 SQL 语句。 对**SQLExecute**或**SQLExecDirect**的调用将返回 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**返回：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 应用程序可以通过调用**SQLGetStmtOption**设置为 SQL_CURSOR_TYPE 来确定目前正在使用的游标类型。 游标类型转换仅适用于一个语句。 下一个**SQLExecDirect**或**SQLExecute**将使用原始语句游标设置完成。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;的游标编程详细信息 &#40;](cursor-programming-details-odbc.md)  
  
  
