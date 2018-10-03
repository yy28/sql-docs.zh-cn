---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b9555c5fd335abcf4069c4ca9241bbade8f71771
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844198"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  通常   
      **SQLFreeStmt**建议不要在 ODBC 3.0 及更高版本。 但是如果应用程序需要重复使用该语句则仍应使用**SQLFreeStmt**与**SQL_RESET_PARAMS**并**SQL_UNBIND**选项)。 您还可以使用[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)， [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)， [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)， [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)，和[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)来替代或复制的函数**SQLFreeStmt**并应改为使用它们。  
  
 一般情况下，它是重复使用比删除它们并分配新的语句更有效。 但是在某些情况下，重复使用的语句，如 SQLFreeStmt 仍必须使用。  
  
## <a name="see-also"></a>请参阅  
 [SQLFreeStmt 函数](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
