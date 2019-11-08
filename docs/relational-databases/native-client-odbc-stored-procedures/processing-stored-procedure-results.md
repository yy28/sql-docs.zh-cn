---
title: 处理存储过程结果 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9240940a05768dfbc577cf0c5ef40a44a1f7c497
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73778929"
---
# <a name="processing-stored-procedure-results"></a>处理存储过程结果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程具有四种用于返回数据的机制：  
  
-   过程中的每一条 SELECT 语句都生成一个结果集。  
  
-   过程可以通过输出参数返回数据。  
  
-   游标输出参数可以回传 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标。  
  
-   过程可以具有整数返回代码。  
  
 应用程序必须能够处理来自存储过程的所有这些输出。 CALL 或 EXECUTE 语句应当包含返回代码和输出参数的参数标记。 使用[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)将它们全部绑定为输出参数，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序将输出值传输到绑定变量。 输出参数和返回代码是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回给客户端的最后一项;在[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)返回 SQL_NO_DATA 之前，不会将它们返回到应用程序。  
  
 ODBC 不支持绑定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标参数。 由于必须在执行过程之前绑定所有输出参数，因此，ODBC 应用程序无法调用包含输出游标参数的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [运行存储过程](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
