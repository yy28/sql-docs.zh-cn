---
title: 使用带有参数的 SQL 语句 |Microsoft 文档
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
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67367fbdd984f0006fd7ed5d4c92d0c696e583a2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-an-sql-statement-with-parameters"></a>使用带参数的 SQL 语句
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要在中处理数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库通过使用在参数中包含的 SQL 语句，你可以使用[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类返回[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)将包含所请求的数据。 若要执行此操作，你必须首先创建 SQLServerPreparedStatement 对象使用[prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。  
  
 构造 SQL 语句时，可使用 ?（问号）字符指定 IN 参数， 该问号将用作随后传递到 SQL 语句中的参数值的占位符。 若要指定参数的值，可以使用 SQLServerPreparedStatement 类的 setter 方法之一。 使用的 setter 方法由要传递到 SQL 语句中的值的数据类型确定。  
  
 向 setter 方法传递值时，不仅需要指定要在 SQL 语句中使用的实际值，还必须指定参数在 SQL 语句中的序数位置。 例如，如果你的 SQL 语句包含一个参数，其序号值将是 1。 如果语句包含两个参数，第一个序号值将是 1，而第二个序号值将是 2。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数进行构造 SQL 语句并将其运行单个字符串参数值，，然后从结果集中读取的结果。  
  
 [!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)  
  
  
