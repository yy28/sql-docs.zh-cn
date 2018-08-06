---
title: 结果集缓存的数据示例 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 487033ade14c5f320b45baba8857c171b94032a4
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278968"
---
# <a name="caching-result-set-data-sample"></a>结果集数据缓存示例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  此 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 示例应用程序说明了如何从数据库中检索大量数据，然后使用 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的 [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 方法控制在客户端中缓存的数据行数。  
  
> [!NOTE]  
>  限制客户端中缓存的行数与限制结果集中包含的总行数不同。 要控制结果集中包含的总行数，请使用 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的 [setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) 方法，该对象具有继承对象 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 对象。  
  
 要对客户端中缓存的行数进行限制，首先必须在创建 Statement 对象时使用服务器端游标，并且在创建 Statement 对象时专门声明要使用的游标类型。 例如，JDBC 驱动程序提供了 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 游标类型，该类型是用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 数据库的快速只进、只读的服务器端游标。  
  
> [!NOTE]  
>  如果不使用 SQL Server 的特定游标类型，也可以使用 selectMethod 连接字符串属性，并将其值设置为“cursor”。 有关 JDBC 驱动程序支持的游标类型的详细信息，请参阅[了解游标类型](../../../connect/jdbc/understanding-cursor-types.md)。  
  
 运行完 Statement 对象中的查询且数据已经以结果集的形式返回到客户端后，可以调用 setFetchSize 方法来控制一次可从数据库中检索的数据量。 例如，某表格包含 100 行数据，提取大小设置为 10，则无论何时，客户端中都仅缓存 10 行数据。 尽管这样会降低数据处理速度，但其优势是所占用的客户端内存较少，这在需要处理大量数据时尤为有用。  
  
 此示例的代码文件名为 CacheRS.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\resultsets  
  
## <a name="requirements"></a>要求  
 若要运行此示例应用程序，必须将 classpath 设置为包含 mssql-jdbc jar 文件。 还将需要访问 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库。 有关如何设置 classpath 的详细信息，请参阅[使用 JDBC 驱动程序](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供要使用的 mssql-jdbc 类库文件，具体使用哪个文件取决于首选的 Java Runtime Environment (JRE) 设置。 若要选择哪个 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码将建立与 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库的连接。 接下来，它会使用带有 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的 SQL 语句，指定服务器端游标类型，然后运行 SQL 语句并将所返回的数据放入 SQLServerResultSet 对象。  
  
 随后，示例代码调用自定义的 timerTest 方法，需要传递的参数为要使用的提取大小和结果集。 timerTest 方法接下来将使用 setFetchSize 方法设置结果集的提取大小，设置测试的起始时间，然后使用 `While` 循环访问结果集。 `While` 循环退出后，该代码立即设置测试的停止时间，然后显示测试结果，其中包括提取大小、已处理的行数以及执行该测试所用的时间。  
  
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class CacheRS {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, SQLServerResultSet.CONCUR_READ_ONLY);) {

            String SQL = "SELECT * FROM Sales.SalesOrderDetail;";

            // Perform a fetch for every row in the result set.
            ResultSet rs = stmt.executeQuery(SQL);
            timerTest(1, rs);
            rs.close();

            // Perform a fetch for every tenth row in the result set.
            rs = stmt.executeQuery(SQL);
            timerTest(10, rs);
            rs.close();

            // Perform a fetch for every 100th row in the result set.
            rs = stmt.executeQuery(SQL);
            timerTest(100, rs);
            rs.close();

            // Perform a fetch for every 1000th row in the result set.
            rs = stmt.executeQuery(SQL);
            timerTest(1000, rs);
            rs.close();

            // Perform a fetch for every 128th row (the default) in the result set.
            rs = stmt.executeQuery(SQL);
            timerTest(0, rs);
            rs.close();
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void timerTest(int fetchSize,
            ResultSet rs) throws SQLException {

        // Declare the variables for tracking the row count and elapsed time.
        int rowCount = 0;
        long startTime = 0;
        long stopTime = 0;
        long runTime = 0;

        // Set the fetch size then iterate through the result set to
        // cache the data locally.
        rs.setFetchSize(fetchSize);
        startTime = System.currentTimeMillis();
        while (rs.next()) {
            rowCount++;
        }
        stopTime = System.currentTimeMillis();
        runTime = stopTime - startTime;

        // Display the results of the timer test.
        System.out.println("FETCH SIZE: " + rs.getFetchSize());
        System.out.println("ROWS PROCESSED: " + rowCount);
        System.out.println("TIME TO EXECUTE: " + runTime);
        System.out.println();
    }
}
```  
  
## <a name="see-also"></a>另请参阅  
 [使用结果集](../../../connect/jdbc/working-with-result-sets.md)  
  
  
