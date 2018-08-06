---
title: 结果集检索数据示例 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb68f2bedb680f990e2b0c4e4e559191915dd300
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279058"
---
# <a name="retrieving-result-set-data-sample"></a>结果集数据检索示例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  此 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 示例应用程序说明了如何从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 数据库中检索一组数据，然后将这些数据显示出来。  
  
 此示例的代码文件名为 RetrieveRS.java，可在以下位置找到该文件：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\resultsets  
  
## <a name="requirements"></a>要求  
 若要运行此示例应用程序，必须将 classpath 设置为包含 mssql-jdbc jar 文件。 还将需要访问 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库。 有关如何设置 classpath 的详细信息，请参阅[使用 JDBC 驱动程序](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供要使用的 mssql-jdbc 类库文件，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 若要选择哪个 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码将建立与 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库的连接。 然后，该代码通过对 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象使用 SQL 语句，运行该 SQL 语句，并将其返回的数据放入 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中。  
  
 接下来，示例代码调用自定义的 displayRow 方法来循环访问结果集中的数据行，并使用 [getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 方法显示其中的某些数据。
  
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class RetrieveRS {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            String SQL = "SELECT * FROM Production.Product;";
            ResultSet rs = stmt.executeQuery(SQL);
            displayRow("PRODUCTS", rs);
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
            System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));
        }
    }
}
```  
  
## <a name="see-also"></a>另请参阅  
 [使用结果集](../../../connect/jdbc/working-with-result-sets.md)  
  
  
