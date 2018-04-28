---
title: 使用保存点 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dccc8739a02fa478c153bbbe1702b925942f8efd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-savepoints"></a>使用保存点
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  保存点提供了回滚部分事务的机制。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可以使用 SAVE TRANSACTION savepoint_name 语句创建一个保存点。 然后，运行 ROLLBACK TRANSACTION savepoint_name 语句回滚到保存点，而不是回滚到事务的开始。  
  
 保存点在不可能发生错误的情况下很有用。 在不频繁发生错误的情况下使用保存点回滚部分事务，其效果好于在执行更新前测试各事务以查看更新是否有效。 更新和回滚都是耗费大量资源的操作，因此，仅当遇到错误的可能性很低，且预先检查更新有效性的成本相对较高时，保存点才会有效。  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持保存点通过使用[setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 通过使用 setSavepoint 方法，你可以创建在当前事务中，保存已命名或未命名的点，并且该方法将返回[SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md)对象。 一个事务中可创建多个保存点。 若要到给定的保存点回滚事务，你可以 SQLServerSavepoint 对象传递给[回滚 (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md)方法。  
  
 在下面的示例中，保存点时执行本地事务包含两个单独的语句中使用`try`块。 语句运行中的 Production.ScrapReason 表[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]使用示例数据库和保存点回滚第二个语句。 这会导致只有第一个语句提交给数据库。  
  
 [!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
