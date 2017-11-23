---
title: "步骤 3： 连接到 SQL 使用 Java 的概念证明 |Microsoft 文档"
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
ms.assetid: 1504a348-1774-47ab-8967-288ec3985ae4
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6bdda6d24e2f1437eb251315d5b91efc7ab1016d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-java"></a>步骤 3： 连接到 SQL 使用 Java 的概念证明
  
此示例中，应考虑仅概念证明。 示例代码为清楚起见，简化，并不一定表示 Microsoft 推荐的最佳做法。  
  
## <a name="step-1--connect"></a>步骤 1： 连接  
  
连接类用于连接到 SQL 数据库。   
  
```java  
  
    // Use the JDBC driver  
    import java.sql.*;  
    import com.microsoft.sqlserver.jdbc.*;  
      
        public class SQLDatabaseConnection {  
      
            // Connect to your database.  
            // Replace server name, username, and password with your credentials  
            public static void main(String[] args) {  
                String connectionString =  
                    "jdbc:sqlserver://yourserver.database.windows.net:1433;"  
                    + "database=AdventureWorks;"  
                    + "user=yourusername@yourserver;"  
                    + "password=yourpassword;"  
                    + "encrypt=true;"  
                    + "trustServerCertificate=false;"  
                    + "hostNameInCertificate=*.database.windows.net;"  
                    + "loginTimeout=30;";  
              
                // Declare the JDBC objects.  
                Connection connection = null;  
                              
                try {  
                    connection = DriverManager.getConnection(connectionString);  
      
                }  
                catch (Exception e) {  
                    e.printStackTrace();  
                }  
                finally {  
                    if (connection != null) try { connection.close(); } catch(Exception e) {}  
                }  
            }  
        }  
```  
  
## <a name="step-2-execute-a-query"></a>步骤 2： 执行查询  
在此示例中，连接到 Azure SQL 数据库、 执行 SELECT 语句，并返回所选的行。   
  
```java  
    // Use the JDBC driver  
    import java.sql.*;  
    import com.microsoft.sqlserver.jdbc.*;  
      
        public class SQLDatabaseConnection {  
      
            // Connect to your database.  
            // Replace server name, username, and password with your credentials  
            public static void main(String[] args) {  
                String connectionString =  
                    "jdbc:sqlserver://yourserver.database.windows.net:1433;"  
                    + "database=AdventureWorks;"  
                    + "user=yourusername@yourserver;"  
                    + "password=yourpassword;"  
                    + "encrypt=true;"  
                    + "trustServerCertificate=false;"  
                    + "hostNameInCertificate=*.database.windows.net;"  
                    + "loginTimeout=30;";  
              
                // Declare the JDBC objects.  
                Connection connection = null;  
                Statement statement = null;   
                ResultSet resultSet = null;  
                              
                try {  
                    connection = DriverManager.getConnection(connectionString);  
      
                    // Create and execute a SELECT SQL statement.  
                    String selectSql = "SELECT TOP 10 Title, FirstName, LastName from SalesLT.Customer";  
                    statement = connection.createStatement();  
                    resultSet = statement.executeQuery(selectSql);  
      
                    // Print results from select statement  
                    while (resultSet.next())   
                    {  
                        System.out.println(resultSet.getString(2) + " "  
                            + resultSet.getString(3));  
                    }  
                }  
                catch (Exception e) {  
                    e.printStackTrace();  
                }  
                finally {  
                    // Close the connections after the data has been handled.  
                    if (resultSet != null) try { resultSet.close(); } catch(Exception e) {}  
                    if (statement != null) try { statement.close(); } catch(Exception e) {}  
                    if (connection != null) try { connection.close(); } catch(Exception e) {}  
                }  
            }  
        }  
```  
  
## <a name="step-3-insert-a-row"></a>步骤 3： 插入行  
在此示例中，执行 INSERT 语句，传递参数，然后检索自动生成主键值。   
  
```java  
    // Use the JDBC driver  
    import java.sql.*;  
    import com.microsoft.sqlserver.jdbc.*;  
      
        public class SQLDatabaseConnection {  
      
            // Connect to your database.  
            // Replace server name, username, and password with your credentials  
            public static void main(String[] args) {  
                String connectionString =  
                    "jdbc:sqlserver://yourserver.database.windows.net:1433;"  
                    + "database=AdventureWorks;"  
                    + "user=yourusername@yourserver;"  
                    + "password=yourpassword;"  
                    + "encrypt=true;"  
                    + "trustServerCertificate=false;"  
                    + "hostNameInCertificate=*.database.windows.net;"  
                    + "loginTimeout=30;";  
              
                // Declare the JDBC objects.  
                Connection connection = null;  
                Statement statement = null;   
                ResultSet resultSet = null;  
                PreparedStatement prepsInsertProduct = null;  
                  
                try {  
                    connection = DriverManager.getConnection(connectionString);  
      
                    // Create and execute an INSERT SQL prepared statement.  
                    String insertSql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES "  
                        + "('NewBike', 'BikeNew', 'Blue', 50, 120, '2016-01-01');";  
      
                    prepsInsertProduct = connection.prepareStatement(  
                        insertSql,  
                        Statement.RETURN_GENERATED_KEYS);  
                    prepsInsertProduct.execute();  
                      
                    // Retrieve the generated key from the insert.  
                    resultSet = prepsInsertProduct.getGeneratedKeys();  
                      
                    // Print the ID of the inserted row.  
                    while (resultSet.next()) {  
                        System.out.println("Generated: " + resultSet.getString(1));  
                    }  
                }  
                catch (Exception e) {  
                    e.printStackTrace();  
                }  
                finally {  
                    // Close the connections after the data has been handled.  
                    if (prepsInsertProduct != null) try { prepsInsertProduct.close(); } catch(Exception e) {}  
                    if (resultSet != null) try { resultSet.close(); } catch(Exception e) {}  
                    if (statement != null) try { statement.close(); } catch(Exception e) {}  
                    if (connection != null) try { connection.close(); } catch(Exception e) {}  
                }  
            }  
        }  
```  
  
## <a name="additional-samples"></a>其他示例  
[示例 JDBC 驱动程序应用程序](../../connect/jdbc/sample-jdbc-driver-applications.md)
