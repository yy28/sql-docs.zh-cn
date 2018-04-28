---
title: 数据源示例 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3475257e4120f53df1d622abafadb5493c9f474a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="data-source-sample"></a>数据源示例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  这[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]示例应用程序演示如何连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用数据源对象的数据库。 它还演示如何检索数据从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用存储的过程的数据库。  
  
 此示例的代码文件名为 connectDS.java，该文件可在以下位置找到：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \samples\connections  
  
## <a name="requirements"></a>需求  
 若要运行此示例应用程序，必须设置类路径来包括 sqljdbc.jar 或 sqljdbc4.jar 文件。 如果 classpath 缺少 sqljdbc.jar 项或 sqljdbc4.jar 项，示例应用程序将引发“找不到类”的常见异常。 你还将需要访问[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库。 有关如何设置类路径的详细信息，请参阅[使用 JDBC 驱动程序](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 类库文件，以便根据你首选的 Java Runtime Environment (JRE) 设置来使用。 有关要选择的 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>示例  
 在下面的示例中，示例代码所设置的使用的 setter 方法的各种连接属性[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)对象，然后调用[getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)方法要返回的 SQLServerDataSource 对象[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)对象。  
  
 接下来，示例代码使用[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) SQLServerConnection 要创建的对象的方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)对象，然后[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)调用方法来执行存储的过程。  
  
 最后，此示例使用[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)从要循环访问该存储过程返回的结果的 executeQuery 方法返回的对象。  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class connectDS {  
  
   public static void main(String[] args) {  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      CallableStatement cstmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.   
         SQLServerDataSource ds = new SQLServerDataSource();  
         ds.setUser("UserName");  
         ds.setPassword("*****");  
         ds.setServerName("localhost");  
         ds.setPortNumber(1433);   
         ds.setDatabaseName("AdventureWorks");  
         con = ds.getConnection();  
  
         // Execute a stored procedure that returns some data.  
         cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");  
         cstmt.setInt(1, 50);  
         rs = cstmt.executeQuery();  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println("EMPLOYEE: " + rs.getString("LastName") +   
               ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER: " + rs.getString("ManagerLastName") +   
               ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
         }  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (cstmt != null) try { cstmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
         System.exit(1);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [连接和检索数据](../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  
