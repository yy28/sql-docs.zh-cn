---
title: "使用多个结果集 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e76f30f5c6b7eb16351749086173bdceaa49f938
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="using-multiple-result-sets"></a>使用多个结果集
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用内联 SQL 时或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]存储过程返回多个结果集，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)中的方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类检索每个返回的数据集。 此外，当运行语句返回多个结果集时，你可以使用[执行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)SQLServerStatement 方法类，因为它将返回**布尔**值，该值指示如果返回值是结果集或更新计数。  
  
 如果 execute 方法返回**true**，运行该语句返回了一个或多个结果集。 你可以访问的第一个结果集通过调用 getResultSet 方法。 若要确定是否提供更多的结果集，你可以调用[getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)方法，它返回**布尔**值**true**是否有多个结果集。 如果多个结果集可用，你可以调用 getResultSet 方法再次对其进行访问，继续该过程，直到处理完所有结果集。 如果 getMoreResults 方法返回**false**，有没有多个结果集到进程。  
  
 如果 execute 方法返回**false**，运行该语句返回了一个更新计数值，其可以通过调用检索[getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)方法。  
  
> [!NOTE]  
>  有关更新计数的详细信息，请参阅[存储过程使用更新的计数](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数，并构造 SQL 语句的运行时，返回两个结果集：  
  
 [!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]  
  
 在这种情况下，返回的结果集的数目为 2。 但是，如此编写代码是为了在返回了未知数目的结果集时，例如在调用存储过程时，这些结果集也会全部得到处理。 若要查看调用存储的过程返回多个结果集，以及更新值的示例，请参阅[处理复杂语句](../../connect/jdbc/handling-complex-statements.md)。  
  
> [!NOTE]  
>  当您对 SQLServerStatement 类 getMoreResults 方法的调用，先前返回的结果集是隐式关闭。  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
