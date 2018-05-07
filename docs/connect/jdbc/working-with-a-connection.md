---
title: 使用连接 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbcd46cd9da1ab189aeafe77c7275aa103ea51f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-a-connection"></a>使用连接
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  下列各节提供了连接到的不同方法的示例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用数据库[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。  
  
> [!NOTE]  
>  如果你有连接到的问题[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用 JDBC 驱动程序，请参阅[故障排除连接](../../connect/jdbc/troubleshooting-connectivity.md)以获取有关如何更正它的建议。  
  
## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>使用 DriverManager 类创建连接  
 创建到连接的最简单方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库是负载的 JDBC 驱动程序并调用驱动程序管理器类，如以下所示的 getConnection 方法：  
  
```  
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 此技术将通过使用驱动程序列表中第一个可以与给定 URL 成功连接的可用驱动程序，创建数据库连接。  
  
> [!NOTE]  
>  在使用的 sqljdbc4.jar 类库时，应用程序不需要显式注册或通过使用 Class.forName 方法加载的驱动程序。 当调用驱动程序管理器类的 getConnection 方法时，合适的驱动程序位于从已注册的 JDBC 驱动程序集。 有关详细信息，请参阅“使用 JDBC Driver”。  
  
## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>使用 SQLServerDriver 类创建连接  
 如果你必须指定特定驱动程序的驱动程序列表中的驱动程序管理器，你可以通过使用创建数据库连接[连接](../../connect/jdbc/reference/connect-method-sqlserverdriver.md)方法[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md)类，如以下所示：  
  
```  
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```  
  
## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>使用 SQLServerDataSource 类创建连接  
 如果必须通过使用创建的连接[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)类，你可以使用各种 setter 方法的类调用之前[getConnection](../../connect/jdbc/reference/getconnection-method.md)方法，如以下所示：  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);   
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```  
  
## <a name="creating-a-connection-that-targets-a-very-specific-data-source"></a>创建目标为非常特殊的数据源的连接  
 如果必须创建目标为非常特殊的数据源的数据库连接，可以采用多种方法。 每种方法取决于使用此连接 URL 设置的属性。  
  
 若要连接到远程服务器上的默认实例，请使用：  
  
 `String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"`  
  
 若要连接到服务器上的特定端口，请使用：  
  
 `String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"`  
  
 若要连接到服务器上的指定实例，请使用：  
  
 `String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"`  
  
 若要连接到服务器上的特定数据库，请使用：  
  
 `String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"`  
  
 有关更多连接 URL 示例，请参阅[生成连接 URL](../../connect/jdbc/building-the-connection-url.md)。  
  
## <a name="creating-a-connection-with-a-custom-login-time-out"></a>创建具有自定义登录超时的连接  
 如果必须调节服务器负载或网络流量，可以创建具有特定登录超时值（以秒为单位）的连接，如下所示：  
  
 `String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"`  
  
## <a name="create-a-connection-with-application-level-identity"></a>创建具有应用程序级别标识的连接  
 如果必须记录日志并进行分析，则必须将连接标识为源于特定应用程序，如下所示：  
  
 `String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"`  
  
## <a name="closing-a-connection"></a>关闭连接  
 你可显式关闭数据库连接，通过调用[关闭](../../connect/jdbc/reference/close-method-sqlserverconnection.md)SQLServerConnection 类，如以下所示的方法：  
  
 `con.close();`  
  
 这将释放该 SQLServerConnection 对象正在使用，数据库资源，或将连接返回到连接池在共用的情况下。  
  
> [!NOTE]  
>  调用 close 方法将还回滚任何挂起的事务。  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
