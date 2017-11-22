---
title: "释放语句句柄 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c1d18006b85b8017600504b02ed9b557b34befa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="freeing-a-statement-handle"></a>释放语句句柄
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  重用语句句柄比删除它们后再分配新句柄更高效。 对语句句柄执行新 SQL 语句之前，应用程序应当验证当前语句设置是否正确。 这些设置包括语句属性、参数绑定和结果集绑定。 通常情况下，参数和结果设置为旧的 SQL 语句必须通过调用未绑定[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) SQL_RESET_PARAMS 与 SQL_UNBIND 选项，然后重新绑定对于新的 SQL 语句。  
  
 当使用语句完成后应用程序时，它将调用[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)以释放该语句。 请注意， **SQLDisconnect**自动释放连接上的所有语句。  
  
## <a name="see-also"></a>另请参阅  
 [正在执行查询 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
