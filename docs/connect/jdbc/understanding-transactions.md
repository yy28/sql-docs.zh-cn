---
title: 了解事务 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d5a6caa9c9bf1766b59aa813719d1461b6ef1aa
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027342"
---
# <a name="understanding-transactions"></a>了解事务

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

事务是组合到工作的逻辑单位的操作组。 它们用于控制和维护事务中的各项操作的一致性和完整性（尽管系统中可能发生错误）。

对于 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，事务可以是本地的，也可以是分布式的。 事务还可以使用隔离级别。 有关 JDBC 驱动程序支持的隔离级别的详细信息, 请参阅[了解隔离级别](../../connect/jdbc/understanding-isolation-levels.md)。

应用程序应使用 Transact-SQL 语句或 JDBC Driver 提供的方法来控制事务，但不可同时使用二者。 对同一事务既使用 Transact-SQL 语句又使用 JDBC API 方法可能会导致问题，例如无法在预期的时间提交事务，提交或回滚事务后又意外地开始了一个新的事务，或者出现“无法继续执行该事务”异常。

## <a name="using-local-transactions"></a>使用本地事务

当事务是单步提交事务时，该事务被视为本地的，并由数据库直接进行处理。 JDBC 驱动程序通过使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的各种方法支持本地事务，这些方法包括 [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)、[commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 和 [rollback](../../connect/jdbc/reference/rollback-method.md)。 本地事务通常由应用程序显式管理，或者由 Java Platform, Enterprise Edition (Java EE) 应用程序服务器自动管理。

以下示例执行 `try` 块中包含两个独立语句的本地事务。 这些语句将对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中的 Production.ScrapReason 表运行，并且如果没有引发异常，则将其提交。 如果引发异常，`catch` 块中的代码将回滚此事务。

[!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]

## <a name="using-distributed-transactions"></a>使用分布式事务

分布式事务可在两个或多个联网的数据库上更新数据，同时保留事务处理的重要的原子性、一致性、独立性和稳定性 (ACID) 等属性。 JDBC 2.0 Optional API 规范中的 JDBC API 添加了分布式事务支持。 分布式事务的管理通常由 Java EE 应用程序服务器环境中的 Java Transaction Service (JTS) 事务管理器自动执行。 但是，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持任意 Java Transaction API (JTA) 兼容的事务管理器下的分布式事务。

JDBC 驱动程序与 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 分布式事务处理协调器 (MS DTC) 无缝集成，为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供真正的分布式事务处理支持。 MS DTC 是 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 为 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 系统提供的分布式事务处理工具。 MS DTC 使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 推出的久经考验的事务处理技术来支持 XA 功能，例如完整的两步分布式提交协议和分布式事务的恢复。

有关如何使用分布式事务的详细信息, 请参阅[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)。

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
