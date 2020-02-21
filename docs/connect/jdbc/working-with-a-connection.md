---
title: 使用连接 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 267605b6a89f323570cfacfc66517b028ef716a2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69025474"
---
# <a name="working-with-a-connection"></a>处理连接

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

以下各部分提供了使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类来连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的不同方法的示例。

> [!NOTE]  
> 如果在使用 JDBC 驱动程序连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时遇到问题，请参阅[连接疑难解答](../../connect/jdbc/troubleshooting-connectivity.md)获取有关解决方法的建议。

## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>使用 DriverManager 类创建连接

创建到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接的最简便方法是加载 JDBC 驱动程序，然后调用 DriverManager 类的 getConnection 方法，如下所示：

```java
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```

此技术将通过使用驱动程序列表中第一个可以与给定 URL 成功连接的可用驱动程序，创建数据库连接。

> [!NOTE]  
> 使用 sqljdbc4.jar 类库时，应用程序无需使用 Class.forName 方法显式注册或加载驱动程序。 调用 DriverManager 类的 getConnection 方法时，会从已注册的 JDBC 驱动程序集中找到相应的驱动程序。 有关详细信息，请参阅“使用 JDBC Driver”。

## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>使用 SQLServerDriver 类创建连接

如果必须为 DriverManager 指定驱动程序列表中的特定驱动程序，可以使用 [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) 类的 [connect](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) 方法来创建数据库连接，如下所示：

```java
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```

## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>使用 SQLServerDataSource 类创建连接

如果必须使用 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 类创建连接，可以先使用此类的各种 setter 方法，然后调用 [getConnection](../../connect/jdbc/reference/getconnection-method.md) 方法，如下所示：

```java
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```

## <a name="creating-a-connection-that-targets-a-very-specific-data-source"></a>创建定目标到非常具体的数据源的连接

如果必须创建目标为非常特殊的数据源的数据库连接，可以采用多种方法。 每种方法取决于使用此连接 URL 设置的属性。

若要连接到远程服务器上的默认实例，请使用：

```java
String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"
```

若要连接到服务器上的特定端口，请使用：

```java
String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"
```

若要连接到服务器上的指定实例，请使用：

```java
String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"
```

若要连接到服务器上的特定数据库，请使用：

```java
String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"
```

若要查看更多连接 URL 示例，请参阅[生成连接 URL](../../connect/jdbc/building-the-connection-url.md)。

## <a name="creating-a-connection-with-a-custom-login-time-out"></a>创建有自定义登录超时的连接

如果必须调节服务器负载或网络流量，可以创建具有特定登录超时值（以秒为单位）的连接，如下所示：

```java
String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"
```

## <a name="create-a-connection-with-application-level-identity"></a>创建有应用程序级别标识的连接

如果必须记录日志并进行分析，则必须将连接标识为源于特定应用程序，如下所示：

```java
String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"
```

## <a name="closing-a-connection"></a>关闭连接

可以通过调用 SQLServerConnection 类的 [close](../../connect/jdbc/reference/close-method-sqlserverconnection.md) 方法显式地关闭数据库连接，如下所示：

```java
con.close();
```

这将释放 SQLServerConnection 对象正在使用的数据库资源，或使连接返回到池方案中的连接池。

> [!NOTE]  
> 调用 close 方法还将回滚所有挂起的事务。

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
