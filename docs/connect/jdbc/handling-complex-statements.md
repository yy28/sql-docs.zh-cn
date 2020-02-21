---
title: 处理复杂语句 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ebd2aee0990b744df1420e88f8cc79870b350f2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027991"
---
# <a name="handling-complex-statements"></a>处理复杂语句
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 时，可能必须处理复杂语句，包括运行时动态生成的语句。 复杂语句通常执行多种任务，包括更新、插入和删除。 这类语句可能还会返回多个结果集和输出参数。 在这些情况下，运行该语句的 Java 代码预先可能不知道返回的对象和数据的类型和数目。  
  
 为了有效地处理复杂语句，JDBC 驱动程序提供多种方法查询返回的对象和数据，以便您的应用程序可正确处理这些内容。 处理复杂语句的关键在于 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法。 此方法将返回布尔值  。 当该值为 true 时，从该语句返回的第一个结果为结果集。 当该值为 false 时，返回的第一个结果为更新计数。  
  
 知道返回的对象或数据的类型后，可以使用 [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 或 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 方法处理这些数据。 要继续处理从复杂语句返回的下一个对象或数据，可以调用 [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md) 方法。  
  
 在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，构造一条组合了存储过程调用和 SQL 语句的复杂语句，再运行这些语句，然后使用 `do` 循环处理返回的所有结果集和更新计数。  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
