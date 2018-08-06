---
title: 结果集修改的数据示例 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8dae1363b6715c9d3c9082897bf00cf3eb3e183b
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279168"
---
# <a name="modifying-result-set-data-sample"></a>结果集数据修改示例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 示例应用程序说明了如何从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中检索可更新的数据集。 然后，它使用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的方法在数据集中插入、修改并最终删除一行数据。  
  
 此示例的代码文件名为 UpdateRS.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\resultsets  
  
## <a name="requirements"></a>要求  
 若要运行此示例应用程序，必须将 classpath 设置为包含 mssql-jdbc jar 文件。 还将需要访问 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库。 有关如何设置 classpath 的详细信息，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供要使用的 mssql-jdbc 类库文件，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 若要选择哪个 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码将建立与 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的连接。 然后，该代码通过对 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 对象使用 SQL 语句，运行该 SQL 语句，并将其返回的数据放入可更新的 SQLServerResultSet 对象中。  
  
 接下来，示例代码使用 [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) 方法将结果集游标移动到要插入的行，使用一系列 [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 方法将数据插入新行，然后调用 [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) 方法将新数据行添加回数据库中。  
  
 插入新的数据行后，示例代码使用 SQL 语句检索前面插入的行，然后同时使用 updateString 和 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法更新数据行，并再次将其添加回数据库中。  
  
 最后，示例代码检索前面已更新的数据行，然后使用 [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) 方法将其从数据库中删除。  
  
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateRS {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);) {

            // Create and execute an SQL statement, retrieving an updateable result set.
            String SQL = "SELECT * FROM HumanResources.Department;";
            ResultSet rs = stmt.executeQuery(SQL);

            // Insert a row of data.
            rs.moveToInsertRow();
            rs.updateString("Name", "Accounting");
            rs.updateString("GroupName", "Executive General and Administration");
            rs.updateString("ModifiedDate", "08/01/2006");
            rs.insertRow();

            // Retrieve the inserted row of data and display it.
            SQL = "SELECT * FROM HumanResources.Department WHERE Name = 'Accounting';";
            rs = stmt.executeQuery(SQL);
            displayRow("ADDED ROW", rs);

            // Update the row of data.
            rs.first();
            rs.updateString("GroupName", "Finance");
            rs.updateRow();

            // Retrieve the updated row of data and display it.
            rs = stmt.executeQuery(SQL);
            displayRow("UPDATED ROW", rs);

            // Delete the row of data.
            rs.first();
            rs.deleteRow();
            System.out.println("ROW DELETED");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void displayRow(String title,
            ResultSet rs) throws SQLException {
        System.out.println(title);
        while (rs.next()) {
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));
            System.out.println();
        }
    }
}
```  
  
## <a name="see-also"></a>另请参阅  
 [使用结果集](../../connect/jdbc/working-with-result-sets.md)  
  
  
