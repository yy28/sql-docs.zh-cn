---
title: "使用返回的状态的存储的过程 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8247f7f81e70aafac8d109abe7f8303c8e13f487
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-a-return-status"></a>使用带有返回状态的存储过程
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可以调用的存储的过程是指返回状态或结果参数。 这通常用于指示存储过程执行成功还是失败。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类，可用来调用这种类型的存储过程，并处理它将返回的数据。  
  
 在这种类型的存储过程调用使用 JDBC 驱动程序时，你必须使用`call`结合 SQL 转义序列[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类. 语法`call`与返回状态参数的转义序列包含以下：  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  有关 SQL 转义序列的详细信息，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 构造时`call`转义序列，使用指定的返回状态参数？ 来指定 IN 参数。 此字符，用作一个占位符，供将从存储过程返回的参数值。 若要指定返回状态参数的值，必须指定参数的数据类型使用[registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 类，在执行存储的过程之前的方法。  
  
> [!NOTE]  
>  使用时的 JDBC 驱动程序与 SQL Server 数据库，registerOutParameter 方法中的返回状态参数指定的值将始终为一个整数，你可以指定通过使用 java.sql.Types.INTEGER 数据类型。  
  
 此外，当为返回状态参数的 registerOutParameter 方法传递一个值，你必须指定不仅数据类型用于参数，但还在存储的过程调用中的参数的序号位置。 对于返回状态参数，其序数位置始终为 1，这是因为它始终是调用存储过程时的第一个参数。 尽管 SQLServerCallableStatement 类提供了有关使用参数的名称来指示特定参数的支持，你可以对返回的状态参数使用仅限参数的序号位置数量。  
  
 例如，创建中的以下存储的过程[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库：  
  
```  
CREATE PROCEDURE CheckContactCity  
   (@cityName CHAR(50))  
AS  
BEGIN  
   IF ((SELECT COUNT(*)  
   FROM Person.Address  
   WHERE City = @cityName) > 1)  
   RETURN 1  
ELSE  
   RETURN 0  
END  
```  
  
 该存储过程返回状态值 1 或 0，这取决于是否能在表 Person.Address 中找到 cityName 参数指定的城市。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数，与[执行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法用于调用 CheckContactCity 存储过程：  
  
 [!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [使用存储过程的语句](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

