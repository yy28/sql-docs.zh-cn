---
title: "不使用任何参数的 SQL 语句 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1e7e97fa030c2efd499aebfa054c0e4827d590dc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-an-sql-statement-with-no-parameters"></a>使用不带参数的 SQL 语句
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要在中处理数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库通过使用 SQL 语句包含任何参数，你可以使用[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类返回[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)将包含所请求的数据。 若要执行此操作，你必须首先创建 SQLServerStatement 对象使用[createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数进行构造并运行，将 SQL 语句，然后从结果集中读取的结果。  
  
 [!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]  
  
 有关使用结果集的详细信息，请参阅[管理使用 JDBC 驱动程序的结果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)  
  
  
