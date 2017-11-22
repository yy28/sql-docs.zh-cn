---
title: "检索结果设置数据示例 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: 4c2ddae853f00d63c48670b2c4f5e2abe0b17ea1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="retrieving-result-set-data-sample"></a>结果集数据检索示例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  这[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]示例应用程序演示如何检索一组数据从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库，以及然后显示该数据。  
  
 此示例的代码文件名为 retrieveRS.java，可在以下位置找到该文件：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\resultsets  
  
## <a name="requirements"></a>要求  
 若要运行此示例应用程序，必须将 classpath 设置为包含 sqljdbc.jar 文件或 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc.jar 项或 sqljdbc4.jar 项，示例应用程序将引发“找不到类”的常见异常。 你还将需要访问[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。 有关如何设置类路径的详细信息，请参阅[使用 JDBC 驱动程序](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 类库文件，以便根据你首选的 Java Runtime Environment (JRE) 设置来使用。 有关要选择的 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码建立连接[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。 然后，使用的 SQL 语句[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象，它运行的 SQL 语句并将放到它返回的数据[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
 接下来，该示例代码调用自定义 displayRow 方法来循环访问结果集中包含的数据的行，并使用[getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)方法以显示一些，它包含的数据。  
  
```java
import java.sql.*;  
  
public class retrieveRS {  
  
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
  
         // Create and execute an SQL statement that returns a  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Production.Product;";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
         displayRow("PRODUCTS", rs);  
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
  
   private static void displayRow(String title, ResultSet rs) {  
      try {  
         System.out.println(title);  
         while (rs.next()) {  
            System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用结果集](../../../connect/jdbc/working-with-result-sets.md)  
  
  
