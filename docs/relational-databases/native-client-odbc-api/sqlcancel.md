---
title: SQL取消 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2db2c4b66940a81dd65064ee730cd683e2206a58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302630"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)主题指出，在 ODBC 2.x 中，如果应用程序在未对语句执行处理时调用**SQLCancel，****则 SQLCancel**具有与**SQLFreeStmt**与**使用SQL_CLOSE**选项相同的效果;此行为仅针对完整性而定义，应用程序应调用**SQLFreeStmt**或**SQLCloseCursor**来关闭游标。 但是，即使本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端应用程序将 ODBC API 版本设定为 3.5.x 或更高版本 **，SQLCancel**函数也将使用 ODBC 2.x 行为。  
  
## <a name="see-also"></a>另请参阅  
 [SQL取消](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
