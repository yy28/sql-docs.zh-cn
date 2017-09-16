---
title: "连接 URL 示例 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8de387fce6f7367f4a2154c4bceb8ebe8447b336
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connection-url-sample"></a>连接 URL 示例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  这[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]示例应用程序演示如何连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用连接 URL 的数据库。 它还演示如何检索数据从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用 SQL 语句的数据库。  
  
 此示例的代码文件名为 connectURL.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\connections  
  
## <a name="requirements"></a>要求  
 若要运行此示例应用程序，必须设置类路径来包括 sqljdbc.jar 或 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc.jar 项或 sqljdbc4.jar 项，示例应用程序将引发“找不到类”的常见异常。 你还将需要访问[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库。 有关如何设置类路径的详细信息，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 类库文件，以便根据你首选的 Java Runtime Environment (JRE) 设置来使用。 有关要选择的 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码在连接 URL 中，设置各种连接属性，然后调用要返回的驱动程序管理器类的 getConnection 方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)对象。  
  
 接下来，示例代码使用[createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) SQLServerConnection 要创建的对象的方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)对象，然后[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法调用以执行 SQL 语句。  
  
 最后，此示例使用[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)从要循环访问由 SQL 语句返回的结果的 executeQuery 方法返回的对象。  
  
```java  
import java.sql.*;  
  
public class connectURL {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
         "databaseName=AdventureWorks;user=UserName;password=*****";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns some data.  
         String SQL = "SELECT TOP 10 * FROM Person.Contact";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println(rs.getString(4) + " " + rs.getString(6));  
         }  
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
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [连接和检索数据](../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  
