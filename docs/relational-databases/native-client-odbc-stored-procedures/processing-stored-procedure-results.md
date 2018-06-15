---
title: 处理存储的过程结果 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b3ae5c1d858b153c947347fd8a8bc07f1dd9557c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32944175"
---
# <a name="processing-stored-procedure-results"></a>处理存储过程结果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程具有四种用于返回数据的机制：  
  
-   过程中的每一条 SELECT 语句都生成一个结果集。  
  
-   过程可以通过输出参数返回数据。  
  
-   游标输出参数可以回传 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标。  
  
-   过程可以具有整数返回代码。  
  
 应用程序必须能够处理来自存储过程的所有这些输出。 CALL 或 EXECUTE 语句应当包含返回代码和输出参数的参数标记。 使用[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)以便将它们绑定所有作为输出参数和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序会将输出值传输到绑定变量。 输出参数和返回代码是向客户端返回的最后一个项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 它们不会返回到应用程序之前[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)返回 SQL_NO_DATA。  
  
 ODBC 不支持绑定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标参数。 由于必须在执行过程之前绑定所有输出参数，因此，ODBC 应用程序无法调用包含输出游标参数的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [运行存储过程](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
