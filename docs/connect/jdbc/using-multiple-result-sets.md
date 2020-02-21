---
title: 使用多个结果集 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 802ade7a34eb5c5174efc35032587f801ef12179
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026267"
---
# <a name="using-multiple-result-sets"></a>使用多个结果集

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

使用返回多个结果集的内联 SQL 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程时，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 方法，以检索返回的每个数据集。 此外，当运行返回多个结果集的语句时，可以使用 SQLServerStatement 类的 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法，因为它将返回一个布尔值，该值指示返回的值是结果集还是更新计数  。

如果 execute 方法返回 true，则运行的语句已返回了一个或多个结果集  。 通过调用 getResultSet 方法可以访问第一个结果集。 若要确定是否提供了多个结果集，可以调用 [getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md) 方法，如果提供了多个结果集，则该方法返回布尔值 true   。 如果有多个结果集可用，则可以再次调用 getResultSet 方法进行访问，继续使用这个过程直到所有的结果集都得到处理。 如果 getMoreResults 方法返回 false  ，则没有多个结果集要处理。

如果 execute 方法返回 false，则所运行的语句返回了更新计数值，可以通过调用 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 方法检索此值  。

> [!NOTE]  
> 有关更新计数的详细信息，请参阅[使用带有更新计数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)。

在下面的示例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，并构造一条 SQL 语句，该语句在运行后将返回两个结果集：

[!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]

在这种情况下，返回的结果集的数目为 2。 但是，如此编写代码是为了在返回了未知数目的结果集时，例如在调用存储过程时，这些结果集也会全部得到处理。 若要查看返回多个结果集以及更新值的存储过程的调用示例，请参阅[处理复杂语句](../../connect/jdbc/handling-complex-statements.md)。

> [!NOTE]  
> 调用 SQLServerStatement 类的 getMoreResults 方法时，会隐式关闭以前返回的结果集。

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
