---
title: "使用保持能力 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19dfa43e83b3fe94fa75df6a2713497093a08a96
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-holdability"></a>使用保持能力
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  默认情况下，事务中创建的结果集将在事务提交到数据库后保持打开状态，或在回滚时保持打开状态。 但是，在事务提交后，使结果集关闭有时也会很有用。 若要这样做，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持的结果使用 set 保持能力。  
  
 可以通过使用设置结果集保持能力[setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 设置时保持能力使用 setHoldability 方法，结果集的 ResultSet.HOLD_CURSORS_OVER_COMMIT 保持能力常量或 ResultSet.CLOSE_CURSORS_AT_COMMIT 可用。  
  
 创建语句对象之一时，JDBC Driver 也支持设置保持能力。 创建语句对象时，如果该对象包含带有结果集保持能力参数的重载，则语句对象的保持能力必须与连接的保持能力匹配。 如果不匹配，将引发异常。 这是因为 SQL Server 仅在连接级别支持保持能力。  
  
 结果集的保持能力是都与在创建结果集时仅服务器端游标的时间设置的结果相关联的 SQLServerConnection 对象保持能力。 它不适用于客户端游标。 与客户端游标的所有结果集将始终都具有 ResultSet.HOLD_CURSORS_OVER_COMMIT 的保持能力值。  
  
 对于服务器游标，当连接到 SQL Server 2005 或更高版本时，设置保持能力只会影响该连接上将要创建的新结果集的保持能力。 这意味着，设置保持能力对该连接上以前创建的和已打开的所有结果集的保持能力没有影响。 但是，如果使用 SQL Server 2000，设置保持能力会影响该连接上现有的结果集和将要创建的新结果集的保持能力。  
  
 在下面的示例中，结果集保持能力设置执行本地事务包含中两个单独的语句时`try`块。 语句运行中的 Production.ScrapReason 表[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库。 首先，该示例切换到手动事务模式设置为自动提交**false**。 一旦自动提交模式被禁用，没有 SQL 语句之前，都将提交应用程序调用[提交](../../connect/jdbc/reference/commit-method-sqlserverconnection.md)方法显式。 如果引发异常，catch 块中的代码将回滚此事务。  
  
 [!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [使用 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
