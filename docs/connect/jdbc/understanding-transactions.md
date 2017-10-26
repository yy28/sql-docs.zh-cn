---
title: "了解事务 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64a9539296531bc0d07d79da3613eb953fefa917
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-transactions"></a>了解事务
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  事务是组合到工作的逻辑单位的操作组。 它们用于控制和维护事务中的各项操作的一致性和完整性（尽管系统中可能发生错误）。  
  
 与[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，事务可以是本地或分布式。 事务还可以使用隔离级别。 有关 JDBC 驱动程序支持的隔离级别的详细信息，请参阅[了解隔离级别](../../connect/jdbc/understanding-isolation-levels.md)。  
  
 应用程序应使用 Transact-SQL 语句或 JDBC Driver 提供的方法来控制事务，但不可同时使用二者。 对同一事务既使用 Transact-SQL 语句又使用 JDBC API 方法可能会导致问题，例如无法在预期的时间提交事务，提交或回滚事务后又意外地开始了一个新的事务，或者出现“无法继续执行该事务”异常。  
  
## <a name="using-local-transactions"></a>使用本地事务  
 当事务是单步提交事务时，该事务被视为本地的，并由数据库直接进行处理。 JDBC 驱动程序支持本地事务使用的各种方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类，其中包括[setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)，[提交](../../connect/jdbc/reference/commit-method-sqlserverconnection.md)，和[回滚](../../connect/jdbc/reference/rollback-method.md)。 本地事务通常由应用程序显式管理，或者由 Java Platform, Enterprise Edition (Java EE) 应用程序服务器自动管理。  
  
 下面的示例执行本地事务中的两个单独语句组成`try`块。 语句运行中的 Production.ScrapReason 表[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库，它们是提交如果未引发的异常。 中的代码`catch`块回滚事务，如果引发异常。  
  
 [!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]  
  
## <a name="using-distributed-transactions"></a>使用分布式事务  
 分布式事务可在两个或多个联网的数据库上更新数据，同时保留事务处理的重要的原子性、一致性、独立性和稳定性 (ACID) 等属性。 JDBC 2.0 Optional API 规范中的 JDBC API 添加了分布式事务支持。 分布式事务的管理通常由 Java EE 应用程序服务器环境中的 Java Transaction Service (JTS) 事务管理器自动执行。 但是，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持任何 Java 事务 API (JTA) 符合事务管理器下的分布式的事务。  
  
 与无缝集成的 JDBC 驱动程序[!INCLUDE[msCoName](../../includes/msconame_md.md)]分布式事务处理协调器 (MS DTC) 以提供 true 分布式事务支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 MS DTC 是由提供的分布式的事务功能[!INCLUDE[msCoName](../../includes/msconame_md.md)]为[!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows 系统。 MS DTC 使用经过验证的事务处理项技术[!INCLUDE[msCoName](../../includes/msconame_md.md)]以支持诸如完成两阶段的分布式的提交协议和分布式事务的恢复等 XA 功能。  
  
 有关如何使用分布式的事务的详细信息，请参阅[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  

