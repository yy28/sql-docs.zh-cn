---
title: 修改结果集数据示例 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
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
ms.openlocfilehash: 6538e5019f13d5f69b9b2606d051b916cc9145e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="modifying-result-set-data-sample"></a>结果集数据修改示例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  这[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]示例应用程序演示如何检索中的数据的可更新集[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 然后，使用的方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)对象，它将插入、 修改，然后最后一行数据将从删除的数据集。  
  
 此示例的代码文件名为 updateRS.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\resultsets  
  
## <a name="requirements"></a>需求  
 若要运行此示例应用程序，必须将 classpath 设置为包含 sqljdbc.jar 文件或 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc.jar 项或 sqljdbc4.jar 项，示例应用程序将引发“找不到类”的常见异常。 你还将需要访问[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库。 有关如何设置类路径的详细信息，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 类库文件，以便根据你首选的 Java Runtime Environment (JRE) 设置来使用。 有关要选择的 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码建立连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库。 然后，使用的 SQL 语句[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)对象，它运行的 SQL 语句，并将它返回到可更新的 SQLServerResultSet 对象的数据。  
  
 接下来，示例代码使用[moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)方法来移动的结果集游标插入的行，使用一系列[updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)方法将数据插入新行中，然后调用[insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)方法以保留数据发回数据库的新行。  
  
 在插入新的数据行后, 的示例代码使用的 SQL 语句来检索以前插入的行，，，，然后使用 updateString 的组合和[updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)方法来更新数据行并再次将其保留回数据库中。  
  
 最后，示例代码检索以前更新的行的数据，然后将其删除从数据库使用[deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)方法。  
  
```java
import java.sql.*;  
  
public class updateRS {  
  
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
  
         // Create and execute an SQL statement, retrieving an updateable result set.  
         String SQL = "SELECT * FROM HumanResources.Department;";  
         stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
         rs = stmt.executeQuery(SQL);  
  
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
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));  
            System.out.println();  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用结果集](../../connect/jdbc/working-with-result-sets.md)  
  
  
