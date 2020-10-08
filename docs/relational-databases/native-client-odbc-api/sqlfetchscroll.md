---
description: SQLFetchScroll
title: SQLFetchScroll |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2e1bfb4b513770c231d1ec3018dc21ecf2c63f39
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810373"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SQLFetchScroll** 将向应用程序返回一行数据。 使用 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)设置行集的大小。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序支持所有定义的提取说明 (例如 SQL_FETCH_RELATIVE) ，但具有以下限制：  
  
-   如果为语句定义了只进游标，则必须使用 SQL_FETCH_NEXT，尝试以任何其他方式执行提取都将导致返回错误。  
  
-   仅静态和键集驱动游标支持 SQL_FETCH_BOOKMARK。  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>SQLFetchScroll 对日期和时间增强功能的支持  
 日期/时间类型的结果列值按 [从 SQL 到 C 的转换](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)中所述进行转换。  
  
 有关详细信息，请参阅 [ODBC&#41;&#40;日期和时间改进 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>SQLFetchScroll 对大型 CLR UDT 的支持  
 **SQLFetchScroll** 支持 (udt) 的大型 CLR 用户定义类型。 有关详细信息，请参阅 [&#40;ODBC&#41;的大型 CLR 用户定义类型 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLFetchScroll 函数](../../odbc/reference/syntax/sqlfetchscroll-function.md)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
