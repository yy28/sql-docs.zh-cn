---
title: 使用数据库镜像 (JDBC) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7528a85cd8e2eb258a89e6d7971ce0f80fa90258
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852682"
---
# <a name="using-database-mirroring-jdbc"></a>使用数据库镜像 (JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  数据库镜像主要是用来增加数据库可用性和数据冗余的软件解决方案。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供了隐式支持数据库镜像，以便开发人员不需要编写任何代码或配置数据库时执行任何其他操作。  
  
 数据库镜像，基于每个数据库实现，保留一份[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]备用服务器上的生产数据库。 该服务器根据数据库镜像会话的配置和状态，充当热备用或温备用服务器。 热备份服务器支持不会丢失任何已提交事务的快速故障转移，暖备份服务器支持强制服务（可能会丢失数据）。  
  
 生产数据库就称为*主体*数据库和备用副本称为*镜像*数据库。 主体数据库和镜像数据库必须驻留在单独的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]（服务器实例） 和它们应驻留在单独的计算机上，如果有可能。  
  
 生产服务器实例（称为主服务器）与备份服务器实例（称为镜像服务器）进行通信。 主服务器和镜像服务器充当数据库镜像会话中的伙伴。 如果主体服务器出现故障，镜像服务器可以使其数据库成为主体数据库通过一个称为过程*故障转移*。 例如，Partner_A 和 Partner_B 是两个伙伴服务器，主体数据库最初位于作为主体服务器的 Partner_A 中，镜像数据库位于作为镜像服务器的 Partner_B 中。 如果 Partner_A 脱机，Partner_B 上的数据库可以进行故障转移，成为当前的主体数据库。 当 Partner_A 重新加入镜像会话时，该服务器变为镜像服务器，并且其数据库变为镜像数据库。  
  
 如果 Partner_A 服务器发生了无法恢复的损坏，则可将 Partner_C 服务器联机，充当 Partner_B（此时为主服务器）的镜像服务器。 然而，在这种情况下，客户端应用程序必须包含编程逻辑，以确保更新连接字符串属性，来反映数据库镜像配置中使用的新服务器名称。 否则，连接该服务器将失败。  
  
 备用数据库镜像配置提供不同级别的性能和数据安全，并支持不同形式的故障转移。 有关详细信息，请参阅"概述的数据库镜像"[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="programming-considerations"></a>编程时的注意事项  
 当主体数据库服务器失败时，客户端应用程序则接收错误以响应 API 调用，这指示与数据库之间的连接已丢失。 出现这种情况时，所有未提交的数据库更改都将丢失，当前事务将回滚。 如果发生这种情况，应用程序应关闭连接（或释放数据源对象）并尝试重新将其打开。 进行连接时，新连接将以透明方式重新定向到镜像数据库（此时充当主服务器），而无需客户端修改连接字符串或数据源对象。  
  
 连接刚刚建立时，主服务器将向出现故障转移时要使用的客户端发送其故障转移伙伴的标识。 当应用程序尝试与失败的主服务器建立初始连接时，客户端并不知道故障转移伙伴的标识。 若要允许客户端的机会来处理这种情况下，failoverPartner 连接字符串属性，并选择性地[setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)数据源方法，允许客户端指定的故障转移的标识在其自己的合作伙伴。 该客户端属性仅可在此种情况下使用，如果主服务器可用，则不使用该属性。  
  
> [!NOTE]  
>  当在连接字符串中或使用数据源对象指定 failoverPartner 时，还必须设置 databaseName 属性，否则将引发异常。 如果未显式指定 failoverPartner 和 databaseName，则当主体数据库服务器出现故障时，应用程序将不会尝试进行故障转移。 换句话说，透明重定向只对显式指定了 failoverPartner 和 databaseName 的连接有效。 有关 failoverPartner 和其他连接字符串属性的详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 如果客户端所提供的故障转移伙伴服务器并非引用充当指定数据库故障转移伙伴的服务器，并且所引用的服务器/数据库位于镜像排列中，则服务器将拒绝该连接。 尽管[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)类提供[getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)方法，此方法仅返回连接字符串中指定的故障转移伙伴的名称或setFailoverPartner 方法。 若要检索的当前正在使用的实际故障转移伙伴名称，使用以下[!INCLUDE[tsql](../../includes/tsql_md.md)]语句：  
  
```  
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```  
  
> [!NOTE]  
>  需要更改此语句以使用您的镜像数据库名称。  
  
 应考虑缓存伙伴信息以便更新连接字符串或设计重试策略，以防第一次连接尝试失败。  
  
## <a name="example"></a>示例  
 在下面的实例中，我们首先尝试与主服务器建立连接。 如果连接失败并引发异常，则尝试连接镜像服务器（可能已升级为新的主服务器）。 请注意连接字符串中 failoverPartner 属性的用法。  
  
```  
import java.sql.*;  
  
public class clientFailover {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://serverA:1433;" +  
         "databaseName=AdventureWorks;integratedSecurity=true;" +  
         "failoverPartner=serverB";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
  
      try {  
         // Establish the connection to the principal server.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         System.out.println("Connected to the principal server.");  
  
         // Note that if a failover of serverA occurs here, then an  
         // exception will be thrown and the failover partner will  
         // be used in the first catch block below.  
  
         // Create and execute an SQL statement that inserts some data.  
         stmt = con.createStatement();  
  
         // Note that the following statement assumes that the   
         // TestTable table has been created in the AdventureWorks  
         // sample database.  
         stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
      }  
  
      // Handle any errors that may have occurred.  
      catch (SQLException se) {  
         try {  
            // The connection to the principal server failed,  
            // try the mirror server which may now be the new  
            // principal server.  
            System.out.println("Connection to principal server failed, " +  
            "trying the mirror server.");  
            con = DriverManager.getConnection(connectionUrl);  
            System.out.println("Connected to the new principal server.");  
            stmt = con.createStatement();  
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
         }  
         catch (Exception e) {  
            e.printStackTrace();  
         }  
      }  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      // Close the JDBC objects.  
      finally {  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
