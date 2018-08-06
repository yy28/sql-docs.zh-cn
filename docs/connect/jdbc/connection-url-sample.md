---
title: 连接 URL 示例 |Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00a82318e9fc77b21e9e634e612d5d65a7ed5137
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278659"
---
# <a name="connection-url-sample"></a>连接 URL 示例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 示例应用程序演示了如何使用连接 URL 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库。 还演示了如何使用 SQL 语句从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中检索数据。  
  
 此示例的代码文件名为 ConnectURL.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\connections  
  
## <a name="requirements"></a>要求  
 若要运行此示例应用程序，必须将 classpath 设置为包含 mssql-jdbc jar 文件。 还将需要访问 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库。 有关如何设置 classpath 的详细信息，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供要使用的 mssql-jdbc 类库文件，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 若要选择哪个 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的实例中，示例代码在连接 URL 中设置了多个连接属性，然后调用 DriverManager 类的 getConnection 方法，以返回 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 对象。  
  
 接下来，示例代码使用 SQLServerConnection 对象的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法来创建 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 对象，然后调用 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法来执行 SQL 语句。  
  
 最后，示例代码使用 executeQuery 方法返回的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象来循环访问 SQL 语句返回的结果。  
  
```java  
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ConnectURL {
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            String SQL = "SELECT TOP 10 * FROM Person.Contact";
            ResultSet rs = stmt.executeQuery(SQL);

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println(rs.getString("FirstName") + " " + rs.getString("LastName"));
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
