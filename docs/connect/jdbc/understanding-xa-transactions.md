---
title: 了解 XA 事务
description: Microsoft JDBC Driver for SQL Server 支持 Java 平台 Enterprise Edition/JDBC 2.0 可选分布式事务。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9bcf55fd300c977105229473228955581da7cdd3
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528731"
---
# <a name="understanding-xa-transactions"></a>了解 XA 事务

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供对 Java Platform, Enterprise Edition/JDBC 2.0 可选分布式事务的支持。 从 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 类获取的 JDBC 连接可以参与标准分布式事务处理环境，例如 Java Platform, Enterprise Edition (Java EE) 应用程序服务器。  

在本文中，XA 代表扩展体系结构。

> [!WARNING]  
> 适用于 SQL 的 Microsoft JDBC Driver 4.2（和更高版本）包含现有功能的新的超时选项，以供自动回滚尚未准备好的事务。 有关更多详细信息，请参阅本主题后面将介绍的[为自动回滚尚未准备好的事务配置服务器端超时设置](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide)。  

## <a name="remarks"></a>备注

用于此分布式事务实现的类如下：  
  
| 类                                              | 实现                      | 说明                                       |
| -------------------------------------------------- | ------------------------------- | ------------------------------------------------- |
| com.microsoft.sqlserver.jdbc.SQLServerXADataSource | javax.sql.XADataSource          | 分布式连接的类工厂。    |
| com.microsoft.sqlserver.jdbc.SQLServerXAResource   | javax.transaction.xa.XAResource | 事务管理器的资源适配器。 |
  
> [!NOTE]  
> XA 分布式事务连接默认使用“提交读”隔离级别。  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>XA 事务使用准则和限制  

以下附加准则适用于紧密耦合的事务：  

- 将 XA 事务与 Microsoft 分布式事务处理协调器 (MS DTC) 一起使用时，你可能会注意到 MS DTC 的当前版本不支持紧密结合的 XA 分支行为。 例如，MS DTC 在 XA 分支事务 ID (XID) 与 MS DTC 事务 ID 之间具有一对一的映射，由松散耦合的 XA 分支执行的工作彼此之间是隔离的。  
  
- MS DTC 还支持紧密耦合的 XA 分支，其中全局事务 ID (GTRID) 相同的多个 XA 分支映射到一个 MS DTC 事务 ID。 通过该项支持，多个紧密耦合的 XA 分支可在资源管理器中查看彼此的更改，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
  
- 借助 [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)标志，应用程序可以使用紧密耦合的 XA 事务，这些事务有不同的 XA 分支事务 ID (BQUAL)，但有相同的全局事务 ID (GTRID) 和格式 ID (FormatID)。 为了使用该功能，必须对 XAResource.start 方法的 flags 参数设置 [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)：
  
    ```java
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>配置说明

如果要同时使用 XA 数据源和 Microsoft 分布式事务处理协调器 (MS DTC) 来处理分布式事务，则需要执行以下步骤。  

> [!NOTE]  
> JDBC 分布式事务组件包含在 JDBC 驱动程序安装的 xa 目录中。 这些组件包括 xa_install.sql 和 sqljdbc_xa.dll 文件。  

> [!NOTE]  
> 从 SQL Server 2019 公共预览版 CTP 2.0 开始，JDBC XA 分布式事务组件包含在 SQL Server 引擎中，可以通过系统存储过程启用或禁用。
> 若要使用 JDBC 驱动程序启用必需组件来执行 XA 分布式事务，请执行以下存储过程。
>
> EXEC sp_sqljdbc_xa_install
>
> 若要禁用先前安装的组件，请执行以下存储过程。
>
> EXEC sp_sqljdbc_xa_uninstall

### <a name="running-the-ms-dtc-service"></a>运行 MS DTC 服务

在服务管理器中，MS DTC 服务应标记为“自动”，以确保其在启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务时运行  。 若要为 XA 事务启用 MS DTC，必须执行以下步骤：  
  
在 Windows Vista 和更高版本上：  
  
1. 单击“开始”按钮，在“开始搜索”框中键入 dcomcnfg，然后按 Enter 打开“组件服务”     。 也可以在“开始搜索”框中键入 %windir%\system32\comexp.msc 打开“组件服务”   。  
  
2. 依次展开“组件服务”、“计算机”、“我的电脑”和“分布式事务处理协调器”。  
  
3. 右键单击“本地 DTC”，再选择“属性”   。  
  
4. 单击“本地 DTC 属性”对话框上的“安全”选项卡   。  
  
5. 选中“启用 XA 事务”复选框，然后单击“确定”   。 这将导致 MS DTC 服务重启。
  
6. 再次单击“确定”以关闭“属性”对话框，然后关闭“组件服务”    。  
  
7. 停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后重新启动，确保它与 MS DTC 更改同步。  

### <a name="configuring-the-jdbc-distributed-transaction-components"></a>配置 JDBC 分布式事务组件  

可通过以下步骤配置 JDBC 驱动程序分布式事务组件：  
  
1. 将新 sqljdbc_xa.dll 从 JDBC 驱动程序安装目录复制到每台要参与分布式事务的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的 Binn 目录中。  
  
    > [!NOTE]  
    > 如果将 XA 事务用于 32 位 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则使用 x86 文件夹中的 sqljdbc_xa.dll 文件，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装在 x64 处理器上也不例外。 如果在 x64 处理器上将 XA 事务用于 64 位 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则使用 x64 文件夹中的 sqljdbc_xa.dll 文件。  
  
2. 对每个要参与分布式事务的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例执行数据库脚本 xa_install.sql。 此脚本将安装 sqljdbc_xa.dll 调用的扩展存储过程。 这些扩展存储过程为 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 实现分布式事务和 XA 支持。 需要以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例管理员的身份来运行此脚本。  
  
3. 若要为特定用户授予使用 JDBC 驱动程序参与分布式事务的权限，请将该用户添加至 SqlJDBCXAUser 角色。  
  
在每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上，一次只能配置一个版本的 sqljdbc_xa.dll 程序集。 应用程序可能需要使用不同版本的 JDBC 驱动程序，才能使用 XA 连接来连接到同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 在这种情况下，必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上安装最新的 JDBC 驱动程序附带的 sqljdbc_xa.dll。  
  
有三种方法可验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上当前安装的 sqljdbc_xa.dll 的版本：
  
1. 打开将参与分布式事务处理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的 LOG 目录。 选择并打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的“ERRORLOG”文件。 在“ERRORLOG”文件中搜索“使用‘SQLJDBC_XA.dll’版本 ...”这一短语。  
  
2. 打开将参与分布式事务处理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的 Binn 目录。 选择 sqljdbc_xa.dll 程序集。

    - 在 Windows Vista 或更高版本上：右键单击“sqljdbc_xa.dll”，然后选择“属性”。 然后单击“详细信息”选项卡  。“文件版本”字段显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上当前安装的 sqljdbc_xa.dll 的版本  。  
  
3. 按照下一节的代码示例所示设置日志记录功能。 在输出日志文件中搜索“服务器 XA DLL 版本:...”这一短语。  

### <a name="configuring-server-side-timeout-settings-for-automatic-rollback-of-unprepared-transactions"></a><a name="BKMK_ServerSide"></a>为自动回滚尚未准备好的事务配置服务器端超时设置  

> [!WARNING]  
> 此服务器端选项是适用于 SQL Server 的 Microsoft JDBC Driver 4.2（和更高版本）附带的新功能。 要获取更新后的行为，务必更新服务器上的 sqljdbc_xa.dll。 有关设置客户端超时的详细信息，请参阅 [XAResource.setTransactionTimeout()](https://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html)。  

有两个注册表设置（DWORD 值）来控制分布式事务的超时行为：  
  
- **XADefaultTimeout**（以秒为单位）：在用户未指定任何超时时使用的默认超时值。 默认值为 0。  
  
- **XAMaxTimeout**（以秒为单位）：用户可以设置的最大超时值。 默认值为 0。  
  
这些设置特定用于 SQL Server 实例，应在以下注册表项下创建：  

```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout  
```

> [!NOTE]  
> 对于在 64 位计算机中运行的 32 位 SQL Server，应在以下项的下面创建注册表设置：`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout`
  
将为每个开始的事务设置超时值，并且在超时过期后由 SQL Server 回滚该事务。 超时具体取决于这些注册表设置以及用户通过 XAResource.setTransactionTimeout() 指定的设置。 有关如何解释这些超时值的一些示例如下所示：  
  
- `XADefaultTimeout = 0`、`XAMaxTimeout = 0`
  
     意味着不使用默认超时值，并且在客户端上不强制执行最大超时。 在这种情况下，只有在客户端使用 XAResource.setTransactionTimeout 设置超时的情况下，事务才会有超时。  
  
- `XADefaultTimeout = 60`、`XAMaxTimeout = 0`
  
     表示如果客户端不指定任何超时，所有事务的超时都为 60 秒。 如果客户端指定超时，将使用该超时值。 不强制执行最大值超时值。  
  
- `XADefaultTimeout = 30`、`XAMaxTimeout = 60`
  
     表示如果客户端不指定任何超时，所有事务的超时都为 30 秒。 如果客户端指定了任何超时，则只要此时间小于 60 秒（最大值），就将使用它。  
  
- `XADefaultTimeout = 0`、`XAMaxTimeout = 30`
  
     表示如果客户端不指定任何超时，所有事务的超时都为 30 秒（最大值）。 如果客户端指定了任何超时，则只要此时间小于 30 秒（最大值），就将使用它。  
  
### <a name="upgrading-sqljdbc_xadll"></a>升级 sqljdbc_xa.dll

您在安装新版本的 JDBC 驱动程序时，也应该使用新版本中的 sqljdbc_xa.dll 来升级服务器上的 sqljdbc_xa.dll。  
  
> [!IMPORTANT]  
> 你应在维护时段内或在未处理任何 MS DTC 事务时升级 sqljdbc_xa.dll。
  
1. 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令 DBCC sqljdbc_xa (FREE)  卸载 sqljdbc_xa.dll。  
  
2. 将新 sqljdbc_xa.dll 从 JDBC 驱动程序安装目录复制到每台要参与分布式事务的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的 Binn 目录中。  
  
    当 sqljdbc_xa.dll 中调用扩展过程时，将会加载新 DLL。 不需要重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来加载新定义。  
  
### <a name="configuring-the-user-defined-roles"></a>配置用户定义角色

若要为特定用户授予使用 JDBC 驱动程序参与分布式事务的权限，请将该用户添加至 SqlJDBCXAUser 角色。 例如，使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码将名为“shelby”（SQL 标准登录用户名为“shelby”）的用户添加至 SqlJDBCXAUser 角色：  

```sql
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```

SQL 用户定义的角色是按数据库定义的。 若要出于安全目的创建自己的角色，必须在每个数据库中定义角色，并在每个数据库中添加用户。 主数据库中 SqlJDBCXAUser 角色的定义非常严格，因为该角色用于授予对主数据库中驻留的 SQL JDBC 扩展存储过程的访问权限。 登录到主数据库后，必须先授予单个用户对主数据库的访问权限，然后再授予这些用户对 SqlJDBCXAUser 角色的访问权限。  

## <a name="example"></a>示例  

```java
import java.net.Inet4Address;
import java.sql.*;
import java.util.Random;
import javax.sql.XAConnection;
import javax.transaction.xa.*;
import com.microsoft.sqlserver.jdbc.*;


public class testXA {

    public static void main(String[] args) throws Exception {

        // Create variables for the connection string.
        String prefix = "jdbc:sqlserver://";
        String serverName = "localhost";
        int portNumber = 1433;
        String databaseName = "AdventureWorks";
        String user = "UserName";
        String password = "*****";

        String connectionUrl = prefix + serverName + ":" + portNumber + ";databaseName=" + databaseName + ";user="
                + user + ";password=" + password;

        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {
            stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");

        }
        // Create the XA data source and XA ready connection.
        SQLServerXADataSource ds = new SQLServerXADataSource();
        ds.setUser(user);
        ds.setPassword(password);
        ds.setServerName(serverName);
        ds.setPortNumber(portNumber);
        ds.setDatabaseName(databaseName);

        XAConnection xaCon = ds.getXAConnection();
        try (Connection con = xaCon.getConnection()) {

            // Get a unique Xid object for testing.
            XAResource xaRes = null;
            Xid xid = null;
            xid = XidImpl.getUniqueXid(1);

            // Get the XAResource object and set the timeout value.
            xaRes = xaCon.getXAResource();
            xaRes.setTransactionTimeout(0);

            // Perform the XA transaction.
            System.out.println("Write -> xid = " + xid.toString());
            xaRes.start(xid, XAResource.TMNOFLAGS);
            PreparedStatement pstmt = con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");
            pstmt.setInt(1, 1);
            pstmt.setString(2, xid.toString());
            pstmt.executeUpdate();

            // Commit the transaction.
            xaRes.end(xid, XAResource.TMSUCCESS);
            xaRes.commit(xid, true);
        }
        xaCon.close();

        // Open a new connection and read back the record to verify that it worked.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT * FROM XAMin")) {
            rs.next();
            System.out.println("Read -> xid = " + rs.getString(2));
            stmt.executeUpdate("DROP TABLE XAMin");
        }
    }
}


class XidImpl implements Xid {

    public int formatId;
    public byte[] gtrid;
    public byte[] bqual;

    public byte[] getGlobalTransactionId() {
        return gtrid;
    }

    public byte[] getBranchQualifier() {
        return bqual;
    }

    public int getFormatId() {
        return formatId;
    }

    XidImpl(int formatId, byte[] gtrid, byte[] bqual) {
        this.formatId = formatId;
        this.gtrid = gtrid;
        this.bqual = bqual;
    }

    public String toString() {
        int hexVal;
        StringBuffer sb = new StringBuffer(512);
        sb.append("formatId=" + formatId);
        sb.append(" gtrid(" + gtrid.length + ")={0x");
        for (int i = 0; i < gtrid.length; i++) {
            hexVal = gtrid[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(gtrid[i] & 0xFF));
            else
                sb.append(Integer.toHexString(gtrid[i] & 0xFF));
        }
        sb.append("} bqual(" + bqual.length + ")={0x");
        for (int i = 0; i < bqual.length; i++) {
            hexVal = bqual[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(bqual[i] & 0xFF));
            else
                sb.append(Integer.toHexString(bqual[i] & 0xFF));
        }
        sb.append("}");
        return sb.toString();
    }

    // Returns a globally unique transaction id.
    static byte[] localIP = null;
    static int txnUniqueID = 0;

    static Xid getUniqueXid(int tid) {

        Random rnd = new Random(System.currentTimeMillis());
        txnUniqueID++;
        int txnUID = txnUniqueID;
        int tidID = tid;
        int randID = rnd.nextInt();
        byte[] gtrid = new byte[64];
        byte[] bqual = new byte[64];
        if (null == localIP) {
            try {
                localIP = Inet4Address.getLocalHost().getAddress();
            } catch (Exception ex) {
                localIP = new byte[] {0x01, 0x02, 0x03, 0x04};
            }
        }
        System.arraycopy(localIP, 0, gtrid, 0, 4);
        System.arraycopy(localIP, 0, bqual, 0, 4);

        // Bytes 4 -> 7 - unique transaction id.
        // Bytes 8 ->11 - thread id.
        // Bytes 12->15 - random number generated by using seed from current time in milliseconds.
        for (int i = 0; i <= 3; i++) {
            gtrid[i + 4] = (byte) (txnUID % 0x100);
            bqual[i + 4] = (byte) (txnUID % 0x100);
            txnUID >>= 8;
            gtrid[i + 8] = (byte) (tidID % 0x100);
            bqual[i + 8] = (byte) (tidID % 0x100);
            tidID >>= 8;
            gtrid[i + 12] = (byte) (randID % 0x100);
            bqual[i + 12] = (byte) (randID % 0x100);
            randID >>= 8;
        }
        return new XidImpl(0x1234, gtrid, bqual);
    }
}

```

## <a name="see-also"></a>另请参阅  

[通过 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
