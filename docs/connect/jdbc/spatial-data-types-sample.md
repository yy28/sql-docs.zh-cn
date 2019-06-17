---
title: 空间数据类型示例为 MSSQL JDBC 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b05182b5dbed154aafd86feec9f73e433f569791
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798352"
---
# <a name="spatial-data-types-sample"></a>空间数据类型示例

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

这[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]示例应用程序演示如何创建、 插入和检索空间数据类型 （Geometry 和 Geography）。
  
此示例的代码文件名为 SpatialDataTypes.java，位于以下位置：  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes  
```

## <a name="requirements"></a>要求  

若要运行此示例应用程序，必须设置 classpath 以包含 mssql-jdbc jar 文件。 有关如何设置 classpath 的详细信息，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。  

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供要使用的 mssql-jdbc 类库文件，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 有关选择哪个 JAR 文件的详细信息，请参阅 [JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例

在以下示例中，示例代码创建名为 SpatialDataTypesTable_JDBC_Sample 包含 Geometry 和 'Geography' 列的表。

该示例首先从良好的 Known-文本 (WKT) 表示一个点创建 Geometry 和 'Geography' 对象。 它使用的参数化查询 SQLServerPreparedStatement 来相应地将数据映射到每个列。

最后，此示例将数据插入到表中，并检索它。 WKT 窗体中显示的数据。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import com.microsoft.sqlserver.jdbc.Geography;
import com.microsoft.sqlserver.jdbc.Geometry;
import com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement;
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class SpatialDataTypes {

    private static String tableName = "SpatialDataTypesTable_JDBC_Sample";

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";
        // Establish the connection.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            dropAndCreateTable(stmt);

            // TODO: Implement Sample code
            String geoWKT = "POINT(3 40 5 6)";
            Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
            Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);

            try (SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) con
                    .prepareStatement("insert into " + tableName + " values (?, ?)");) {
                pstmt.setGeometry(1, geomWKT);
                pstmt.setGeography(2, geogWKT);
                pstmt.execute();

                SQLServerResultSet rs = (SQLServerResultSet) stmt.executeQuery("select * from " + tableName);
                rs.next();

                System.out.println("Geometry data: " + rs.getGeometry(1));
                System.out.println("Geography data: " + rs.getGeography(2));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void dropAndCreateTable(Statement stmt) throws SQLException {
        stmt.executeUpdate("if object_id('" + tableName + "','U') is not null" + " drop table " + tableName);

        stmt.executeUpdate("Create table " + tableName + " (c1 geometry, c2 geography)");
    }
}
```

## <a name="see-also"></a>另请参阅  

[使用 JDBC 数据类型](../../connect/jdbc/working-with-data-types-jdbc.md)  
  
