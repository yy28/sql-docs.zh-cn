---
title: 使用数据库镜像 (JDBC) |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2914adb0a69c680624365b7fe0af23f9615f6f05
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798663"
---
# <a name="using-database-mirroring-jdbc"></a>使用数据库镜像 (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

数据库镜像主要是用来增加数据库可用性和数据冗余的软件解决方案。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 为数据库镜像提供了隐式支持，这样，在为数据库配置好该功能后，开发人员便无需编写任何代码或采取任何措施。

数据库镜像是按数据库实现的，它在备用服务器上保留一份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产品数据库的副本。 该服务器根据数据库镜像会话的配置和状态，充当热备用或温备用服务器。 热备份服务器支持不会丢失任何已提交事务的快速故障转移，暖备份服务器支持强制服务（可能会丢失数据）。

产品数据库称为“主体”数据库，备份副本称为“镜像”数据库   。 主体数据库和镜像数据库必须位于不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例（服务器实例）中，如果可能，它们应位于不同的计算机中。

生产服务器实例（称为主服务器）与备份服务器实例（称为镜像服务器）进行通信。 主服务器和镜像服务器充当数据库镜像会话中的伙伴。 如果主体服务器失败，镜像服务器可以通过称为“故障转移”的过程将其数据库转为主体数据库  。 例如，Partner_A 和 Partner_B 为两个伙伴服务器，主数据库最初位于主服务器 Partner_A 上，镜像数据库位于镜像服务器 Partner_B 上。 如果 Partner_A 脱机，则 Partner_B 上的数据库便可通过故障转移而成为当前主数据库。 Partner_A 重新加入镜像会话后，它将成为镜像服务器，而其数据库将成为镜像数据库。

如果 Partner_A 服务器发生了无法恢复的损坏，则可将 Partner_C 服务器联机，充当 Partner_B（此时为主服务器）的镜像服务器。 然而，在这种情况下，客户端应用程序必须包含编程逻辑，以确保更新连接字符串属性，来反映数据库镜像配置中使用的新服务器名称。 否则，连接该服务器将失败。

备用数据库镜像配置提供不同级别的性能和数据安全，并支持不同形式的故障转移。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“数据库镜像概述”。

## <a name="programming-considerations"></a>编程时的注意事项

当主体数据库服务器失败时，客户端应用程序则接收错误以响应 API 调用，这指示与数据库之间的连接已丢失。 出现这种情况时，所有未提交的数据库更改都将丢失，当前事务将回滚。 如果发生这种情况，应用程序应关闭连接（或释放数据源对象）并尝试重新将其打开。 进行连接时，新连接将以透明方式重新定向到镜像数据库（此时充当主服务器），而无需客户端修改连接字符串或数据源对象。

连接刚刚建立时，主服务器将向出现故障转移时要使用的客户端发送其故障转移伙伴的标识。 当应用程序尝试与失败的主服务器建立初始连接时，客户端并不知道故障转移伙伴的标识。 为了使客户端能够应对这种情况，failoverPartner 连接字符串属性以及可选的 [setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 数据源方法都允许客户端在本机指定故障转移伙伴的标识。 该客户端属性仅可在此种情况下使用，如果主服务器可用，则不使用该属性。

> [!NOTE]  
> 当在连接字符串中或使用数据源对象指定 failoverPartner 时，还必须设置 databaseName 属性，否则将引发异常。 如果未显式指定 failoverPartner 和 databaseName，则当主体数据库服务器出现故障时，应用程序将不会尝试进行故障转移。 换句话说，透明重定向只对显式指定了 failoverPartner 和 databaseName 的连接有效。 有关 failoverPartner 和其他连接字符串属性的详细信息，请参阅[连接属性设置](../../connect/jdbc/setting-the-connection-properties.md)。

如果客户端所提供的故障转移伙伴服务器并非引用充当指定数据库故障转移伙伴的服务器，并且所引用的服务器/数据库位于镜像排列中，则服务器将拒绝该连接。 尽管 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 类提供了 [getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md) 方法，但此方法仅返回在此连接字符串或 setFailoverPartner 方法中指定的故障转移伙伴的名称。 若要检索当前使用的实际故障转移伙伴的名称，请使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：

```sql
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```

> [!NOTE]  
> 需要更改此语句以使用您的镜像数据库名称。

应考虑缓存伙伴信息以便更新连接字符串或设计重试策略，以防第一次连接尝试失败。

## <a name="example"></a>示例

在下面的实例中，我们首先尝试与主服务器建立连接。 如果连接失败并引发异常，则尝试连接镜像服务器（可能已升级为新的主服务器）。 请注意连接字符串中 failoverPartner 属性的用法。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class ClientFailover {
    public static void main(String[] args) {

        String connectionUrl = "jdbc:sqlserver://serverA:1433;"
                + "databaseName=AdventureWorks;integratedSecurity=true;"
                + "failoverPartner=serverB";

        // Establish the connection to the principal server.
        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement();) {
            System.out.println("Connected to the principal server.");

            // Note that if a failover of serverA occurs here, then an
            // exception will be thrown and the failover partner will
            // be used in the first catch block below.

            // Execute a SQL statement that inserts some data.

            // Note that the following statement assumes that the
            // TestTable table has been created in the AdventureWorks
            // sample database.
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");
        }
        catch (SQLException se) {
            System.out.println("Connection to principal server failed, " + "trying the mirror server.");
            // The connection to the principal server failed,
            // try the mirror server which may now be the new
            // principal server.
            try (Connection con = DriverManager.getConnection(connectionUrl);
                    Statement stmt = con.createStatement();) {
                System.out.println("Connected to the new principal server.");
                stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");
            }
            // Handle any errors that may have occurred.
            catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
