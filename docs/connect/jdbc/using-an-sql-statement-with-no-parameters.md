---
title: 使用不带参数的 SQL 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d63b7195e2de73292e56f9a63dcce561ca3b906e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790222"
---
# <a name="using-an-sql-statement-with-no-parameters"></a>使用不带参数的 SQL 语句

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要使用不带参数的 SQL 语句处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据，可以使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法返回包含所需数据的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)。 若要执行此操作，必须首先使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法创建一个 SQLServerStatement 对象。

在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，构造并运行一条 SQL 语句，然后从结果集读取结果。

[!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]

有关使用结果集的详细信息，请参阅[JDBC 驱动程序管理结果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)。

## <a name="see-also"></a>另请参阅

[使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)
