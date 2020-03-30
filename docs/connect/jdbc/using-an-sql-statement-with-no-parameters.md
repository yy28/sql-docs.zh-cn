---
title: 使用不含参数的 SQL 语句 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da4342b8640e89a0183a3f80889dd27ecfb1a76e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026545"
---
# <a name="using-an-sql-statement-with-no-parameters"></a>使用不含参数的 SQL 语句

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要使用不带参数的 SQL 语句处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据，可以使用 [SQLServerStatement](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 类的 [executeQuery](../../connect/jdbc/reference/sqlserverstatement-class.md) 方法返回包含所需数据的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)。 若要执行此操作，必须首先使用 [SQLServerConnection](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 类的 [createStatement](../../connect/jdbc/reference/sqlserverconnection-class.md) 方法创建一个 SQLServerStatement 对象。

在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，构造并运行一条 SQL 语句，然后从结果集读取结果。

[!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]

若要详细了解如何使用结果集，请参阅[使用 JDBC 驱动程序管理结果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)。

## <a name="see-also"></a>另请参阅

[使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)
