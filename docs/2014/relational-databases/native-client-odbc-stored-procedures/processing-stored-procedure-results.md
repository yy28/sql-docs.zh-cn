---
title: 处理存储的过程结果 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 3e7ffe8b73a7df4cbe2fddcaa0864e338b039f53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68205484"
---
# <a name="processing-stored-procedure-results"></a>处理存储过程结果
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程具有四种用于返回数据的机制：  
  
-   过程中的每一条 SELECT 语句都生成一个结果集。  
  
-   过程可以通过输出参数返回数据。  
  
-   游标输出参数可以回传 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标。  
  
-   过程可以具有整数返回代码。  
  
 应用程序必须能够处理来自存储过程的所有这些输出。 CALL 或 EXECUTE 语句应当包含返回代码和输出参数的参数标记。 使用[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)以将其绑定所有作为输出参数和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序会将输出值传输到绑定变量。 输出参数和返回代码是返回到客户端的最后一项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 它们不会返回到应用程序之前[SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md)返回 sql_no_data 为止。  
  
 ODBC 不支持绑定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标参数。 由于必须在执行过程之前绑定所有输出参数，因此，ODBC 应用程序无法调用包含输出游标参数的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程。  
  
## <a name="see-also"></a>请参阅  
 [运行存储过程](running-stored-procedures.md)  
  
  
