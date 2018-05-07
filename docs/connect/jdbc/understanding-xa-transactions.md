---
title: 了解 XA 事务 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
caps.latest.revision: 80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a78fdb7edae90289d64d4c7fdf74ac3a12d4b115
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-xa-transactions"></a>了解 XA 事务
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]为 Java 平台，Enterprise Edition/JDBC 2.0 可选分布式事务提供支持。 从获取 JDBC 连接[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md)类可以参与标准的分布式事务处理如 Java 平台企业版 (Java EE) 应用程序服务器的环境。  
  
> [!WARNING]  
>  Microsoft JDBC Driver 4.2 （和更高版本） for SQL 包含新的自动回滚的现有功能的未准备好的事务的超时选项。 请参阅[配置服务器端超时设置的自动回滚撤消事务](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide)本主题中的更多细节更高版本。  
  
## <a name="remarks"></a>注释  
 用于此分布式事务实现的类如下：  
  
|类|实现|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.sqlserver.jdbc.SQLServerXADataSource|javax.sql.XADataSource|分布式连接的类工厂。|  
|com.microsoft.sqlserver.jdbc.SQLServerXAResource|javax.transaction.xa.XAResource|事务管理器的资源适配器。|  
  
> [!NOTE]  
>  XA 分布式事务连接默认使用“提交读”隔离级别。  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>使用 XA 事务的准则和限制  
 以下附加准则适用于紧密耦合的事务：  
  
-   当您将 XA 事务与 Microsoft 分布式事务处理协调器 (MS DTC) 一起使用时，您可能会注意到 MS DTC 的当前版本不支持紧密结合的 XA 分支行为。 例如，MS DTC 在 XA 分支事务 ID (XID) 与 MS DTC 事务 ID 之间具有一对一的映射，由松散耦合的 XA 分支执行的工作彼此之间是隔离的。  
  
     在提供的修补程序[MSDTC 和紧密耦合事务](http://support.microsoft.com/kb/938653)支持其中多个 XA 分支与同一个全局事务 ID (GTRID) 的紧密耦合的 XA 分支映射到单个 MS DTC 事务 id。 此支持多个紧密耦合的 XA 分支看到彼此的所做更改的资源管理器中，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   A [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)标志将允许应用程序以使用紧密耦合的 XA 事务，其具有不同 XA 分支事务 Id (BQUAL)，但具有相同的全局事务 ID (GTRID) 并设置 ID (FormatID) 的格式。 若要使用该功能，必须设置[SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)对 XAResource.start 方法标志参数：  
  
    ```  
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>配置说明  
 如果要同时使用 XA 数据源和 Microsoft 分布式事务处理协调器 (MS DTC) 来处理分布式事务，则需要执行以下步骤。  
  
> [!NOTE]  
>  JDBC 分布式事务组件包含在 JDBC 驱动程序安装的 xa 目录中。 这些组件包括 xa_install.sql 和 sqljdbc_xa.dll 文件。  
  
### <a name="running-the-ms-dtc-service"></a>运行 MS DTC 服务  
 MS DTC 服务应将标记为**自动**在服务管理器以确保它正在运行时[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]服务已启动。 若要为 XA 事务启用 MS DTC，必须执行以下步骤：  
  
 在 Windows Vista 和更高版本上：  
  
1.  单击**启动**按钮，键入**dcomcnfg**中开始**搜索**框中，，然后按 ENTER 以打开**组件服务**。 您还可以键入中的 %windir%\system32\comexp.msc **StartSearch**框以打开**组件服务**。  
  
2.  依次展开“组件服务”、“计算机”、“我的电脑”和“分布式事务处理协调器”。  
  
3.  右键单击**本地 DTC** ，然后选择**属性**。  
  
4.  单击**安全**选项卡上**本地 DTC 属性**对话框。  
  
5.  选择**启用 XA 事务**复选框，并依次**确定**。 这将使 MS DTC 服务重新启动。  
  
6.  单击**确定**以关闭**属性**对话框，然后再关闭**组件服务**。  
  
7.  停止，然后重启[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]若要确保其同步向上与 MS DTC 更改。  
  
### <a name="configuring-the-jdbc-distributed-transaction-components"></a>配置 JDBC 分布式事务组件  
 可通过以下步骤配置 JDBC 驱动程序分布式事务组件：  
  
1.  将新 sqljdbc_xa.dll 从 JDBC 驱动程序安装目录复制到 Binn 目录中的每个[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]计算机将参与分布式事务。  
  
    > [!NOTE]  
    >  如果你在 32 位与使用 XA 事务[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，使用在 x86 sqljdbc_xa.dll 文件文件夹，即使[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]安装在 x64 处理器。 如果你在使用 64 位使用 XA 事务[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]上 x64 处理器，使用在 x64 sqljdbc_xa.dll 文件文件夹。  
  
2.  执行数据库脚本 xa_install.sql 上每个[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例将参与分布式事务。 此脚本将安装 sqljdbc_xa.dll 调用的扩展存储过程。 这些扩展存储的过程实现分布式的事务和 XA 支持[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。 将需要以管理员身份运行此脚本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例。  
  
3.  若要为特定用户授予使用 JDBC 驱动程序参与分布式事务的权限，请将该用户添加至 SqlJDBCXAUser 角色。  
  
 你可以在每个配置 sqljdbc_xa.dll 程序集只有一个版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例一次。 应用程序可能需要使用不同版本的 JDBC 驱动程序连接到相同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过 XA 连接的实例。 在这种情况下，sqljdbc_xa.dll，附带的最新的 JDBC 驱动程序，必须安装在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例。  
  
 有三种方法，以确认服务器上当前安装的版本 sqljdbc_xa.dll[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例：  
  
1.  打开的日志目录[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]计算机将参与分布式事务。 选择并打开[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"查看错误日志"文件。 在“ERRORLOG”文件中搜索“使用‘SQLJDBC_XA.dll’版本 ...”这一短语。  
  
2.  打开的 Binn 目录[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]计算机将参与分布式事务。选择 sqljdbc_xa.dll 程序集。  
  
    -   在 Windows Vista 或更高版本上：右键单击 sqljdbc_xa.dll，然后选择“属性”。 然后单击**详细信息**选项卡。**文件版本**字段显示在当前安装的 sqljdbc_xa.dll 版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例。  
  
3.  按照下一节的代码示例所示设置日志记录功能。 在输出日志文件中搜索“服务器 XA DLL 版本:...”这一短语。  
  
###  <a name="BKMK_ServerSide"></a> 配置服务器端超时设置的自动回滚撤消事务  
  
> [!WARNING]  
>  此服务器端选项是新增功能与 Microsoft JDBC Driver 4.2 （和更高版本） for SQL Server。 若要获取更新的行为，请确保服务器上的 sqljdbc_xa.dll 已更新。 有关设置客户端端超时的详细信息，请参阅[XAResource.setTransactionTimeout()](http://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html)。  
  
 有两个注册表设置（DWORD 值）来控制分布式事务的超时行为：  
  
-   **XADefaultTimeout** （以秒为单位）： 用户未指定任何超时值时要使用的默认超时值。 默认值为 0。  
  
-   **XAMaxTimeout** （以秒为单位）： 用户可以设置的超时值的最大值。 默认值为 0。  
  
 这些设置特定用于 SQL Server 实例，应在以下注册表项下创建：  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL\<**版本**>。\<*instance_name*> \XATimeout  
  
> [!NOTE]  
>  对于在 64 位计算机中运行的 32 位 SQL Server，注册表设置均应下创建以下项： HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL\<版本 >。 < 实例名称 > \XATimeout  
  
 将为每个开始的事务设置超时值，并且在超时过期后由 SQL Server 回滚该事务。 超时具体取决于这些注册表设置以及用户通过 XAResource.setTransactionTimeout() 指定的设置。 有关如何解释这些超时值的一些示例如下所示：  
  
-   XADefaultTimeout = 0，XAMaxTimeout = 0  
  
     意味着不使用默认超时值，并且在客户端上不强制执行最大超时。 在这种情况下，只有在客户端使用 XAResource.setTransactionTimeout 设置超时时，事务才有超时。  
  
-   XADefaultTimeout = 60，XAMaxTimeout = 0  
  
     意味着如果客户端不指定任何超时，所有事务将有 60 秒的超时。 如果客户端指定超时，将使用该超时值。 不强制执行最大值超时值。  
  
-   XADefaultTimeout = 30，XAMaxTimeout = 60  
  
     意味着如果客户端不指定任何超时，所有事务将有 30 秒的超时。 如果客户端指定任何超时，只要超时值小于 60 秒（最大值），将使用客户端的超时。  
  
-   XADefaultTimeout = 0，XAMaxTimeout = 30  
  
     意味着如果客户端不指定任何超时，所有事务将有 30 秒的超时（最大值）。 如果客户端指定任何超时，只要超时值小于 30 秒（最大值），将使用客户端的超时。  
  
### <a name="upgrading-sqljdbcxadll"></a>升级 sqljdbc_xa.dll  
 您在安装新版本的 JDBC 驱动程序时，也应该使用新版本中的 sqljdbc_xa.dll 来升级服务器上的 sqljdbc_xa.dll。  
  
> [!IMPORTANT]  
>  您应该在维护窗口期间或进程中没有 MS DTC 事务时升级 sqljdbc_xa.dll。  
  
1.  卸载 sqljdbc_xa.dll 使用[!INCLUDE[tsql](../../includes/tsql_md.md)]命令**DBCC sqljdbc_xa （免费）**。  
  
2.  将新 sqljdbc_xa.dll 从 JDBC 驱动程序安装目录复制到 Binn 目录中的每个[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]计算机将参与分布式事务。  
  
     当 sqljdbc_xa.dll 中调用扩展过程时，将会加载新 DLL。 不需要重新启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]加载新的定义。  
  
### <a name="configuring-the-user-defined-roles"></a>配置用户定义的角色  
 若要为特定用户授予使用 JDBC 驱动程序参与分布式事务的权限，请将该用户添加至 SqlJDBCXAUser 角色。 例如，使用以下[!INCLUDE[tsql](../../includes/tsql_md.md)]代码以将名为 shelby （名为 shelby 的 SQL 标准登录名用户） 的用户添加到 SqlJDBCXAUser 角色：  
  
```  
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```  
  
 SQL 用户定义的角色是按数据库定义的。 若要出于安全目的创建自己的角色，必须在每个数据库中定义角色，并在每个数据库中添加用户。 主数据库中 SqlJDBCXAUser 角色的定义非常严格，因为该角色用于授予对主数据库中驻留的 SQL JDBC 扩展存储过程的访问权限。 登录到主数据库后，必须先授予单个用户对主数据库的访问权限，然后再授予这些用户对 SqlJDBCXAUser 角色的访问权限。  
  
## <a name="example"></a>示例  
  
```  
import java.net.Inet4Address;  
import java.sql.*;  
import java.util.Random;  
import javax.transaction.xa.*;  
import javax.sql.*;  
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
      String connectionUrl = prefix + serverName + ":" + portNumber  
         + ";databaseName=" + databaseName + ";user=" + user + ";password=" + password;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         Connection con = DriverManager.getConnection(connectionUrl);  
  
         // Create a test table.  
         Statement stmt = con.createStatement();  
         try {  
            stmt.executeUpdate("DROP TABLE XAMin");   
         }  
         catch (Exception e) {  
         }  
         stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");  
         stmt.close();  
         con.close();  
  
         // Create the XA data source and XA ready connection.  
         SQLServerXADataSource ds = new SQLServerXADataSource();  
         ds.setUser(user);  
         ds.setPassword(password);  
         ds.setServerName(serverName);  
         ds.setPortNumber(portNumber);  
         ds.setDatabaseName(databaseName);  
         XAConnection xaCon = ds.getXAConnection();  
         con = xaCon.getConnection();  
  
         // Get a unique Xid object for testing.  
         XAResource xaRes = null;  
         Xid xid = null;  
         xid = XidImpl.getUniqueXid(1);  
  
         // Get the XAResource object and set the timeout value.  
         xaRes = xaCon.getXAResource();  
         xaRes.setTransactionTimeout(0);  
  
         // Perform the XA transaction.  
         System.out.println("Write -> xid = " + xid.toString());  
         xaRes.start(xid,XAResource.TMNOFLAGS);  
         PreparedStatement pstmt =   
         con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");  
         pstmt.setInt(1,1);  
         pstmt.setString(2,xid.toString());  
         pstmt.executeUpdate();  
  
         // Commit the transaction.  
         xaRes.end(xid,XAResource.TMSUCCESS);  
         xaRes.commit(xid,true);  
  
         // Cleanup.  
         con.close();  
         xaCon.close();  
  
         // Open a new connection and read back the record to verify that it worked.  
         con = DriverManager.getConnection(connectionUrl);  
         ResultSet rs = con.createStatement().executeQuery("SELECT * FROM XAMin");  
         rs.next();  
         System.out.println("Read -> xid = " + rs.getString(2));  
         rs.close();  
         con.close();  
      }   
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
  
class XidImpl implements Xid {  
  
   public int formatId;  
   public byte[] gtrid;  
   public byte[] bqual;  
   public byte[] getGlobalTransactionId() {return gtrid;}  
   public byte[] getBranchQualifier() {return bqual;}  
   public int getFormatId() {return formatId;}  
  
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
      for (int i=0; i<gtrid.length; i++) {  
         hexVal = gtrid[i]&0xFF;  
         if ( hexVal < 0x10 )  
            sb.append("0" + Integer.toHexString(gtrid[i]&0xFF));  
         else  
            sb.append(Integer.toHexString(gtrid[i]&0xFF));  
         }  
         sb.append("} bqual(" + bqual.length + ")={0x");  
         for (int i=0; i<bqual.length; i++) {  
            hexVal = bqual[i]&0xFF;  
            if ( hexVal < 0x10 )  
               sb.append("0" + Integer.toHexString(bqual[i]&0xFF));  
            else  
               sb.append(Integer.toHexString(bqual[i]&0xFF));  
         }  
         sb.append("}");  
         return sb.toString();  
      }  
  
      // Returns a globally unique transaction id.  
      static byte [] localIP = null;  
      static int txnUniqueID = 0;  
      static Xid getUniqueXid(int tid) {  
  
      Random rnd = new Random(System.currentTimeMillis());  
      txnUniqueID++;  
      int txnUID = txnUniqueID;  
      int tidID = tid;  
      int randID = rnd.nextInt();  
      byte[] gtrid = new byte[64];  
      byte[] bqual = new byte[64];  
      if ( null == localIP) {  
         try {  
            localIP = Inet4Address.getLocalHost().getAddress();  
         }  
         catch ( Exception ex ) {  
            localIP =  new byte[] { 0x01,0x02,0x03,0x04 };  
         }  
      }  
      System.arraycopy(localIP,0,gtrid,0,4);  
      System.arraycopy(localIP,0,bqual,0,4);  
  
      // Bytes 4 -> 7 - unique transaction id.  
      // Bytes 8 ->11 - thread id.  
      // Bytes 12->15 - random number generated by using seed from current time in milliseconds.  
      for (int i=0; i<=3; i++) {  
         gtrid[i+4] = (byte)(txnUID%0x100);  
         bqual[i+4] = (byte)(txnUID%0x100);  
         txnUID >>= 8;  
         gtrid[i+8] = (byte)(tidID%0x100);  
         bqual[i+8] = (byte)(tidID%0x100);  
         tidID >>= 8;  
         gtrid[i+12] = (byte)(randID%0x100);  
         bqual[i+12] = (byte)(randID%0x100);  
         randID >>= 8;  
      }  
      return new XidImpl(0x1234, gtrid, bqual);  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序执行事务](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
