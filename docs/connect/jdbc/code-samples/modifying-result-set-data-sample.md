---
title: 结果集修改的数据示例 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e46eec18eca6123839034fec1fb5b3e5aadbcd0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624035"
---
# <a name="modifying-result-set-data-sample"></a>结果集数据修改示例

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 示例应用程序展示了如何从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库检索一组可更新的数据。 然后，它使用 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的方法在数据集中插入、修改并最终删除一行数据。

此示例的代码文件名为“UpdateResultSet.java”，位于以下位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>要求

若要运行此示例应用程序，必须设置 classpath 以包含 mssql-jdbc jar 文件。 还将需要访问 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库。 有关如何设置 classpath 的详细信息，请参阅[使用 JDBC 驱动程序](../../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供要使用的 mssql-jdbc 类库文件，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 若要选择哪个 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>示例

在下面的示例中，示例代码将建立与 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库的连接。 然后，它结合使用 SQL 语句和 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象，运行 SQL 语句，并将自己返回的数据放入可更新的 SQLServerResultSet 对象中。

接下来，示例代码使用 [moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) 方法将结果集游标移动到要插入的行，使用一系列 [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 方法将数据插入新行，然后调用 [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) 方法将新数据行添加回数据库中。

插入新的数据行后，示例代码使用 SQL 语句检索前面插入的行，然后同时使用 updateString 和 [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法更新数据行，并再次将其添加回数据库中。

最后，示例代码检索前面已更新的数据行，然后使用 [deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) 方法将其从数据库中删除。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateResultSet {

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

[使用结果集](../../../connect/jdbc/code-samples/working-with-result-sets.md)
