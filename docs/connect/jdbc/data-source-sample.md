---
title: 数据源示例 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9b5da0ee2138296a4b0c7bf12e6e33a06d029cd
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785256"
---
# <a name="data-source-sample"></a>数据源示例

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 示例应用程序说明了如何使用数据源对象连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。 还说明了如何使用存储过程从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中检索数据。

此示例的代码文件名为“ConnectDataSource.java”，位于以下位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>要求

若要运行此示例应用程序，必须设置 classpath 以包含 mssql-jdbc jar 文件。 还将需要访问 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库。 有关如何设置 classpath 的详细信息，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供要使用的 mssql-jdbc 类库文件，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 若要选择哪个 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>示例

在下面的实例中，示例代码使用 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象的 setter 方法设置各种连接属性，然后调用 SQLServerDataSource 对象的 [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) 方法，以返回 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 对象。

接下来，示例代码使用 SQLServerConnection 对象的 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法来创建 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 对象，然后调用 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) 方法来执行存储过程。

最后，示例代码使用 executeQuery 方法返回的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象来循环访问存储过程返回的结果。

```java
import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class ConnectDataSource {

    public static void main(String[] args) {

        // Create datasource.
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setUser("<user>");
        ds.setPassword("<password>");
        ds.setServerName("<server>");
        ds.setPortNumber(<port>);
        ds.setDatabaseName("AdventureWorks");

        try (Connection con = ds.getConnection();
                CallableStatement cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");) {
            // Execute a stored procedure that returns some data.
            cstmt.setInt(1, 50);
            ResultSet rs = cstmt.executeQuery();

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println("EMPLOYEE: " + rs.getString("LastName") + ", " + rs.getString("FirstName"));
                System.out.println("MANAGER: " + rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));
                System.out.println();
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## <a name="see-also"></a>另请参阅

[连接和检索数据](../../connect/jdbc/connecting-and-retrieving-data.md)
