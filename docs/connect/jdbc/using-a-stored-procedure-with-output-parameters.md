---
title: 使用存储的过程使用输出参数 |Microsoft 文档
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
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: adc77f65d20f409d0ad2ff115031d02888876863
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>使用带有输出参数的存储过程
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可以调用的存储的过程是返回一个或多个 OUT 参数，它们是存储的过程使用以返回数据的参数返回到调用应用程序。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类，该类可用于调用这种类型的存储过程以及如何处理，它返回的数据。  
  
 在这种类型的存储过程调用使用 JDBC 驱动程序时，必须使用`call`一起使用的 SQL 转义序列[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 语法`call`使用 OUT 参数的转义序列包含以下：  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  有关 SQL 转义序列的详细信息，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 构造时`call`转义序列，通过使用指定的扩展参数？ 来指定 IN 参数。 此字符充当要从该存储过程返回的参数值的占位符。 若要指定 OUT 参数的值，必须指定每个参数的数据类型使用[registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 类之前运行存储的过程的方法。  
  
 指定在 registerOutParameter 方法 OUT 参数必须是包含在 java.sql.Types，反过来映射到本机之一的 JDBC 数据类型之一的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。 JDBC 有关详细信息和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型，请参阅[了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)。  
  
 当为 OUT 参数的 registerOutParameter 方法传递一个值时，你必须指定不仅数据类型用于参数，但还参数的序号放置或存储过程中的参数的名称。 例如，如果存储过程包含单个 OUT 参数，则其序数值为 1；如果存储过程包含两个参数，则第一个序数值为 1，第二个序数值为 2。  
  
> [!NOTE]  
>  JDBC 驱动程序不支持的光标、 SQLVARIANT、 表和时间戳使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型作为输出参数。  
  
 例如，创建中的以下存储的过程[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库：  
  
```  
CREATE PROCEDURE GetImmediateManager  
   @employeeID INT,  
   @managerID INT OUTPUT  
AS  
BEGIN  
   SELECT @managerID = ManagerID   
   FROM HumanResources.Employee   
   WHERE EmployeeID = @employeeID  
END  
```  
  
 根据指定的整数 IN 参数 (employeeID)，该存储过程也返回单个整数 OUT 参数 (managerID)。 根据 HumanResources.Employee 表中包含的 EmployeeID，OUT 参数中返回的值为 ManagerID。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数，与[执行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法用于调用 GetImmediateManager 存储过程：  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt(1, 5);  
      cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt(2));  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
 本示例使用序号位置来标识参数。 或者，也可以使用参数的名称（而非其序号位置）来标识此参数。 下面的代码示例修改了上一个示例，以说明如何在 Java 应用程序中使用命名参数。 请注意，这些参数名称对应于存储过程的定义中的参数名称：  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt("employeeID", 5);  
      cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
      cstmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
```  
  
 }  
  
> [!NOTE]  
>  这些示例使用 SQLServerCallableStatement 类的 execute 方法运行存储的过程。 使用此方法是因为存储过程也不会返回结果集。 如果它这样做， [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)将使用方法。  
  
 存储过程可能返回更新计数和多个结果集。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]遵循 JDBC 3.0 规范，哪些状态之前检索到 OUT 参数，应检索多个结果集和更新的计数。 即，应用程序应检索的所有结果集对象和更新之前使用 CallableStatement.getter 方法检索扩展参数计数。 否则，结果集对象和尚未检索的更新计数将会丢失时检索到 OUT 参数。 有关更新计数的详细信息和多个结果集，请参阅[存储过程使用更新的计数](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)和[使用多个结果集](../../connect/jdbc/using-multiple-result-sets.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在存储过程中使用语句](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
