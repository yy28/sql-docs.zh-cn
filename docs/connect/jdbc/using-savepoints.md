---
title: 使用保存点 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd1ab1ab51a1fa7214d704ab6152af9368c0c67a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695925"
---
# <a name="using-savepoints"></a>使用保存点

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

保存点提供了回滚部分事务的机制。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，可以使用 SAVE TRANSACTION savepoint_name 语句创建保存点。 然后，运行 ROLLBACK TRANSACTION savepoint_name 语句回滚到保存点，而不是回滚到事务的开始。

保存点在不可能发生错误的情况下很有用。 在不频繁发生错误的情况下使用保存点回滚部分事务，其效果好于在执行更新前测试各事务以查看更新是否有效。 更新和回滚都是耗费大量资源的操作，因此，仅当遇到错误的可能性很低，且预先检查更新有效性的成本相对较高时，保存点才会有效。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持通过 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md) 方法来使用保存点。 通过使用 setSavepoint 方法，可以在当前事务中创建命名或未命名的保存点，并且该方法将返回 [SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md) 对象。 一个事务中可创建多个保存点。 要将事务回滚到指定的保存点，可以将 SQLServerSavepoint 对象传递给 [rollback (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md) 方法。

下面的实例中，将在执行 `try` 块中包含两个独立语句的本地事务时使用保存点。 该语句将根据 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中的表 Production.ScrapReason 来运行，并使用保存点回滚第二个语句。 这会导致只有第一个语句提交给数据库。

[!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
