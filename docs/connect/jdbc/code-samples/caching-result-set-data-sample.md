---
title: "缓存结果设置数据示例 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 29ef11c103d357bf9d73555b6d41f1a4125e6aa9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="caching-result-set-data-sample"></a>结果集数据缓存示例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  这[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]示例应用程序演示如何从数据库检索大量数据，然后控制使用的缓存客户端的数据的行数[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
> [!NOTE]  
>  限制客户端中缓存的行数与限制结果集中包含的总行数不同。 若要控制包含在结果集中的行的总数，使用[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)方法[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象，两个继承[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)对象。  
  
 以数目的客户端上高速缓存行上设置的限制，必须首先使用服务器端游标时特别指出创建语句对象时要使用的游标类型创建语句对象之一。 例如，JDBC 驱动程序提供 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 游标类型，这是快速只进、 只读的服务器端游标用于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库。  
  
> [!NOTE]  
>  如果不使用 SQL Server 的特定游标类型，也可以使用 selectMethod 连接字符串属性，并将其值设置为“cursor”。 有关支持的 JDBC 驱动程序的光标类型的详细信息，请参阅[了解游标类型](../../../connect/jdbc/understanding-cursor-types.md)。  
  
 已运行该语句对象中包含的查询和数据就会归还客户端作为结果集后，你可以调用要控制一次从数据库中检索的数据量的 setFetchSize 方法。 例如，某表格包含 100 行数据，提取大小设置为 10，则无论何时，客户端中都仅缓存 10 行数据。 尽管这样会降低数据处理速度，但其优势是所占用的客户端内存较少，这在需要处理大量数据时尤为有用。  
  
 此示例的代码文件名为 cacheRS.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\resultsets  
  
## <a name="requirements"></a>要求  
 若要运行此示例应用程序，必须将 classpath 设置为包含 sqljdbc.jar 文件或 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc.jar 项或 sqljdbc4.jar 项，示例应用程序将引发“找不到类”的常见异常。 你还将需要访问[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。 有关如何设置类路径的详细信息，请参阅[使用 JDBC 驱动程序](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 类库文件，以便根据你首选的 Java Runtime Environment (JRE) 设置来使用。 有关要选择的 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码建立连接[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。 然后，它使用的 SQL 语句[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象，指定的服务器端游标类型，然后运行 SQL 语句，并将它返回到 SQLServerResultSet 对象的数据。  
  
 接下来，该示例代码调用自定义 timerTest 方法，将作为参数传递提取大小给使用，并将结果集。 TimerTest 方法然后设置结果集通过 setFetchSize 方法的提取大小、 设置的测试的开始时间，然后循环访问结果集与`While`循环。 只要`While`退出循环时，代码设置的停止时间的测试，然后显示包括提取大小，处理的行数测试的结果并执行测试所花费的时间。  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;  
  
public class cacheRS {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
            "databaseName=AdventureWorks;integratedSecurity=true;";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns a large  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Sales.SalesOrderDetail;";  
         stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, +  
               SQLServerResultSet.CONCUR_READ_ONLY);  
  
         // Perform a fetch for every row in the result set.  
         rs = stmt.executeQuery(SQL);  
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
      catch (Exception e) {  
         e.printStackTrace();  
      }  
  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
  
   private static void timerTest(int fetchSize, ResultSet rs) {  
      try {  
  
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
  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用结果集](../../../connect/jdbc/working-with-result-sets.md)  
  
  
