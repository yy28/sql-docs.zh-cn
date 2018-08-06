---
title: 使用带有输出参数的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d040dd53d646a455e3623b2a0ee33406ea4574c5
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278618"
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>使用带有输出参数的存储过程
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  可以调用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 存储过程是返回一个或多个 OUT 参数的存储过程，存储过程使用这些参数将数据返回到调用它的应用程序。 可以使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供的 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类，调用此类存储过程并处理其返回的数据。  
  
 使用 JDBC 驱动程序调用此类存储过程时，必须结合 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法使用 `call` SQL 转义序列。 带有 OUT 参数的 `call` 转义序列的语法如下所示：  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  有关 SQL 转义序列的详细信息，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 构造时`call`转义序列，使用指定 OUT 参数？ 来指定 IN 参数。 此字符充当要从该存储过程返回的参数值的占位符。 要为 OUT 参数指定值，必须在运行存储过程前使用 SQLServerCallableStatement 类的 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 方法指定各参数的数据类型。  
  
 使用 registerOutParameter 方法为 OUT 参数指定的值必须是 java.sql.Types 所包含的 JDBC 数据类型之一，而它又被映射成本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据类型之一。 有关 JDBC 详细信息和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型，请参阅[了解 JDBC 驱动程序的数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)。  
  
 对于 OUT 参数向 registerOutParameter 方法传递一个值时，不仅必须指定要用于此参数的数据类型，而且必须在存储过程中指定此参数的序号位置或此参数的名称。 例如，如果存储过程包含单个 OUT 参数，则其序数值为 1；如果存储过程包含两个参数，则第一个序数值为 1，第二个序数值为 2。  
  
> [!NOTE]  
>  JDBC 驱动程序不支持将 CURSOR、SQLVARIANT、TABLE 和 TIMESTAMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据类型用作 OUT 参数。  
  
 作为示例，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中创建以下存储过程：  
  
```sql
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
  
 在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，然后使用 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法调用 GetImmediateManager 存储过程：  
  
```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");) {  
        cstmt.setInt(1, 5);  
        cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt(2));  
    }  
} 
```  
  
 本示例使用序号位置来标识参数。 或者，也可以使用参数的名称（而非其序号位置）来标识此参数。 下面的代码示例修改了上一个示例，以说明如何在 Java 应用程序中使用命名参数。 请注意，这些参数名称对应于存储过程的定义中的参数名称：  
  
```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}"); ) {  
        cstmt.setInt("employeeID", 5);  
        cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
    }  
}
```  
  
> [!NOTE]  
>  这些示例使用 SQLServerCallableStatement 类的 execute 方法来运行存储的过程。 使用此方法是因为存储过程也不会返回结果集。 如果返回，则使用 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法。  
  
 存储过程可能返回更新计数和多个结果集。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 遵循 JDBC 3.0 规范，此规范规定在检索 OUT 参数之前应检索多个结果集和更新计数。 也就是说，应用程序应检索所有结果集对象和更新计数，然后使用 CallableStatement.getter 方法检索 OUT 参数。 否则，当检索 OUT 参数时，尚未检索的 ResultSet 对象和更新计数将丢失。 有关更新计数的详细信息和多个结果集，请参阅[使用带有更新计数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)并[使用多个结果集](../../connect/jdbc/using-multiple-result-sets.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在存储过程中使用语句](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
