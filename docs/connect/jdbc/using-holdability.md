---
title: 使用保持能力 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c126385955ce6e9fa9098ec5a09ba115b94ffb0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026201"
---
# <a name="using-holdability"></a>使用可保持性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

默认情况下，事务中创建的结果集将在事务提交到数据库后保持打开状态，或在回滚时保持打开状态。 但是，在事务提交后，使结果集关闭有时也会很有用。 为此，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持使用结果集的保持能力。

可通过使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 方法设置结果集的保持能力。 使用 setHoldability 方法设置保持能力时，可使用 `ResultSet.HOLD_CURSORS_OVER_COMMIT` 或 `ResultSet.CLOSE_CURSORS_AT_COMMIT` 的结果集保持能力的常量。

创建语句对象之一时，JDBC Driver 也支持设置保持能力。 创建语句对象时，如果该对象包含带有结果集保持能力参数的重载，则语句对象的保持能力必须与连接的保持能力匹配。 如果不匹配，将引发异常。 这是因为 SQL Server 仅在连接级别支持保持能力。

结果集的保持能力是在仅为服务器端游标创建结果集时，与结果集相关联的 SQLServerConnection 对象的保持能力。 它不适用于客户端游标。 所有具有客户端游标的结果集将始终具有值为 `ResultSet.HOLD_CURSORS_OVER_COMMIT` 的保持能力。

对于服务器游标，当连接到 SQL Server 2005 或更高版本时，设置保持能力只会影响该连接上将要创建的新结果集的保持能力。 这意味着，设置保持能力对该连接上以前创建的和已打开的所有结果集的保持能力没有影响。

在下面的示例中，结果集的保持能力将在执行 `try` 块中包含两个单独语句的本地事务时进行设置。 这些语句将对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中的 Production.ScrapReason 表运行。 首先，示例通过将自动提交设置为 `false` 来切换到手动事务模式。 禁用自动提交模式后，在应用程序显式调用 [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 方法之前，不会提交任何 SQL 语句。 如果引发异常，catch 块中的代码将回滚此事务。

[!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
