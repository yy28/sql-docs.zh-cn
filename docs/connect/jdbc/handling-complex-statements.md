---
title: "处理复杂语句 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf7d2c48d091c013a351ae1f0421f172e33bb37e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="handling-complex-statements"></a>处理复杂语句
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  当你使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，你可能需要处理复杂语句，其中包括在运行时动态生成的语句。 复杂语句通常执行多种任务，包括更新、插入和删除。 这类语句可能还会返回多个结果集和输出参数。 在这些情况下，运行该语句的 Java 代码预先可能不知道返回的对象和数据的类型和数目。  
  
 为了有效地处理复杂语句，JDBC 驱动程序提供多种方法查询返回的对象和数据，以便您的应用程序可正确处理这些内容。 处理复杂语句的关键是[执行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类。 此方法返回**布尔**值。 当该值为 true 时，从该语句返回的第一个结果为结果集。 当该值为 false 时，返回的第一个结果为更新计数。  
  
 在你知道类型的对象或返回的数据，你可以使用[getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)或[getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)方法来处理该数据。 若要继续到下一个对象或从复杂语句返回的数据，你可以调用[getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md)方法。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数的复杂语句构造将存储的过程调用和 SQL 语句结合起来，运行语句，然后`do`循环是用于处理所有结果集，并更新返回的计数。  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [语句使用 JDBC 驱动程序](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  

