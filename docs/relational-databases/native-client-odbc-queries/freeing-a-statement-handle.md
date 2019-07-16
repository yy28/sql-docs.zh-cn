---
title: 释放语句句柄 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6304cbfb0db7204a2bc641d01012c32c727e35fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058723"
---
# <a name="freeing-a-statement-handle"></a>释放语句句柄
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  重用语句句柄比删除它们后再分配新句柄更高效。 对语句句柄执行新 SQL 语句之前，应用程序应当验证当前语句设置是否正确。 这些设置包括语句属性、参数绑定和结果集绑定。 通常情况下，参数和结果集的旧的 SQL 语句必须通过调用未绑定[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) SQL_RESET_PARAMS 和 SQL_UNBIND 选项，然后重新绑定为新的 SQL 语句。  
  
 当应用程序使用完该语句时，它将调用[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)释放语句。 请注意， **SQLDisconnect**自动释放连接上的所有语句。  
  
## <a name="see-also"></a>请参阅  
 [执行查询&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
