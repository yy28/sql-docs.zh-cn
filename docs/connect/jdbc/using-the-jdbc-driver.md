---
title: 使用 JDBC 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e0f803b68f2ab9f62c3df27c6930da8e3a8a4a0
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737088"
---
# <a name="using-the-jdbc-driver"></a>使用 JDBC 驱动程序

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本部分提供使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库建立简单连接的快速入门指导。 在连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库之前，必须首先在本地计算机或服务器上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并且必须在本地计算机上安装 JDBC 驱动程序。  
  
## <a name="choosing-the-right-jar-file"></a>选择正确的 JAR 文件

Microsoft JDBC Driver 提供了不同 Jar 下使用与您的首选 Java Runtime Environment (JRE) 设置的对应关系中：

提供了 SQL Server 的 Microsoft JDBC 驱动程序 7.2 **mssql jdbc 7.2.0.jre8.jar**，并**mssql jdbc 7.2.0.jre11.jar**类库文件。

SQL Server 的 Microsoft JDBC 驱动程序 7.0 提供了**mssql jdbc 7.0.0.jre8.jar**，并**mssql jdbc 7.0.0.jre10.jar**类库文件。

Microsoft JDBC Driver 6.4 for SQL Server 提供了**mssql jdbc 6.4.0.jre7.jar**， **mssql jdbc 6.4.0.jre8.jar**，并**mssql jdbc 6.4.0.jre9.jar**类库文件。

Microsoft JDBC Driver 6.2 for SQL Server 提供了**mssql-6.2.2.jre7.jar**，并**mssql jdbc 6.2.2.jre8.jar**类库文件。
  
Microsoft JDBC Drivers 6.0 和 4.2 for SQL Server 提供了**sqljdbc41.jar**，并**sqljdbc42.jar**类库文件。
  
Microsoft JDBC Driver 4.1 for SQL Server 提供了**sqljdbc41.jar**类库文件。

你的选择还将确定可用功能。 若要选择哪个 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="setting-the-classpath"></a>设置 Classpath

Microsoft JDBC 驱动程序 jar 文件不是 Java SDK 的一部分，并且必须包含在用户应用程序的 Classpath 中。

如果使用 JDBC Driver 4.1 或 4.2 中，将 classpath 设置为包括**sqljdbc41.jar**或**sqljdbc42.jar**从相应的驱动程序下载的文件。

如果使用 JDBC Driver 6.2 classpath 设置为包含**mssql-6.2.2.jre7.jar**或**mssql jdbc 6.2.2.jre8.jar**。

如果使用 JDBC Driver 6.4 classpath 设置为包含**mssql jdbc 6.4.0.jre7.jar**，* * mssql jdbc 6.4.0.jre8.jar 或**mssql jdbc 6.4.0.jre9.jar**。

如果使用 JDBC 驱动程序 7.0 classpath 设置为包含**mssql jdbc 7.0.0.jre8.jar**或**mssql jdbc 7.0.0.jre10.jar**。

如果使用 JDBC 驱动程序 7.2 classpath 设置为包含**mssql jdbc 7.2.0.jre8.jar**或**mssql jdbc 7.2.0.jre11.jar**。

如果 classpath 缺少正确的 Jar 文件的条目，则应用程序将引发常见`Class not found`异常。  

### <a name="for-microsoft-jdbc-driver-72"></a>Microsoft JDBC 驱动程序 7.2

**Mssql jdbc 7.2.0.jre8.jar**或**mssql jdbc 7.2.0.jre11.jar**文件安装在以下位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.2.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.2.0.jre11.jar
```

以下代码片段是用于 Windows 应用程序的 CLASSPATH 语句示例：

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.2 for SQL Server\sqljdbc_7.2\enu\mssql-jdbc-7.2.0.jre11.jar`

以下代码片段是用于 Unix/Linux 应用程序的 CLASSPATH 语句示例：

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.2/enu/mssql-jdbc-7.2.0.jre11.jar`

请确保 CLASSPATH 语句包含一个[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，如任一**mssql jdbc 7.2.0.jre8.jar**或**mssql jdbc 7.2.0.jre11.jar**。
  
### <a name="for-microsoft-jdbc-driver-70"></a>Microsoft JDBC 驱动程序 7.0

**Mssql jdbc 7.0.0.jre8.jar**或**mssql jdbc 7.0.0.jre10.jar**文件安装在以下位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre10.jar
```

以下代码片段是用于 Windows 应用程序的 CLASSPATH 语句示例：  

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.0 for SQL Server\sqljdbc_7.0\enu\mssql-jdbc-7.0.0.jre10.jar`  
  
以下代码片段是用于 Unix/Linux 应用程序的 CLASSPATH 语句示例：  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.0/enu/mssql-jdbc-7.0.0.jre10.jar`  
  
请确保 CLASSPATH 语句包含一个[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，如任一**mssql jdbc 7.0.0.jre8.jar**或**mssql jdbc 7.0.0.jre10.jar**。

### <a name="for-microsoft-jdbc-driver-64"></a>有关 Microsoft JDBC Driver 6.4

**Mssql jdbc 6.4.0.jre7.jar**，* * mssql jdbc 6.4.0.jre8.jar 或**mssql jdbc 6.4.0.jre9.jar**文件安装在以下位置：  

```bash  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre9.jar
```

以下代码片段是用于 Windows 应用程序的 CLASSPATH 语句示例：  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
以下代码片段是用于 Unix/Linux 应用程序的 CLASSPATH 语句示例：  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
请确保 CLASSPATH 语句包含一个[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，如任一**mssql jdbc 6.4.0.jre7.jar**，* * mssql jdbc 6.4.0.jre8.jar 或**mssql jdbc 6.4.0.jre9.jar**。

### <a name="for-microsoft-jdbc-driver-62"></a>有关 Microsoft JDBC Driver 6.2

**Mssql-6.2.2.jre7.jar**或**mssql jdbc 6.2.2.jre8.jar**文件安装在以下位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre8.jar
```

以下代码片段是用于 Windows 应用程序的 CLASSPATH 语句示例：  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.2.jre8.jar`  
  
以下代码片段是用于 Unix/Linux 应用程序的 CLASSPATH 语句示例：  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.2.jre8.jar`  
  
请确保 CLASSPATH 语句包含只有一个[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 mssql-6.2.2.jre7.jar 或 mssql jdbc 6.2.2.jre8.jar。  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>Microsoft JDBC 驱动程序 4.1、 4.2 和 6.0

Sqljdbc.jar 文件、sqljdbc4.jar 文件、sqljdbc41.jar 或 sqljdbc42.jar 文件安装在以下位置：  

```bash
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc4.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc41.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc42.jar  
```

以下代码片段是用于 Windows 应用程序的 CLASSPATH 语句示例：  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
以下代码片段是用于 Unix/Linux 应用程序的 CLASSPATH 语句示例：  

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
必须确保 CLASSPATH 语句只包含一个 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 sqljdbc.jar、sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar。  
  
> [!NOTE]  
> 在 Windows 系统上，长度超过 8.3 文件名约定的目录名称或带有空格的文件夹名称可能会导致类路径问题。 如果你怀疑存在这些类型的问题，应将 sqljdbc.jar 文件、sqljdbc4.jar 文件或 sqljdbc41.jar 文件暂时移到简单的目录名称（例如 `C:\Temp`）中，更改类路径，然后确定是否已解决该问题。  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>直接在命令提示符运行的应用程序

classpath 是在操作系统中配置的。 将 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 追加到系统的 classpath 中。 或者，可使用 `java -classpath` 选项，在运行此应用程序的 Java 命令行上指定 classpath。  
  
### <a name="applications-that-run-in-an-ide"></a>在 IDE 中运行的应用程序  

每个 IDE 供应商都提供了在 IDE 中设置 classpath 的不同方法。 仅在操作系统中设置 classpath 将无法正常工作。 必须将 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 添加到 IDE 类路径。  
  
### <a name="servlets-and-jsps"></a>Servlet 和 JSP  

Servlet 和 JSP 在 servlet/JSP 引擎（如 Tomcat）中运行。 必须根据 servlet/JSP 引擎文档来设置 classpath。 仅在操作系统中设置 classpath 将无法正常工作。 一些 servlet/JSP 引擎提供了设置屏幕，用于设置引擎的 classpath。 在这种情况下，必须将正确的 JDBC 驱动程序 JAR 文件追加到现有的引擎 classpath，然后重新启动引擎。 在其他情况下，通过在引擎安装期间将 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 复制到 lib 之类的特定目录，可以部署此驱动程序。 也可以在引擎专用的配置文件中指定引擎驱动程序的 classpath。  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  

Enterprise Java Bean (EJB) 在 EJB 容器中运行。 EJB 容器来自多家供应商。 Java 小程序在浏览器中运行，但是从 Web 服务器上下载的。 将 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 复制到 Web 服务器根并在小程序的 HTML 存档选项卡中指定 JAR 文件的名称，例如 `<applet ... archive=mssql-jdbc-***.jar>`。  
  
## <a name="making-a-simple-connection-to-a-database"></a>与数据库建立简单连接

使用 sqljdbc.jar 类库时，应用程序必须首先按如下所示注册驱动程序：  
  
`Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  

加载驱动程序，可以通过使用连接 URL 和驱动程序管理器类的 getConnection 方法来建立连接：

```java
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```

从 JDBC API 4.0 开始，`DriverManager.getConnection()` 方法得到了增强，可自动加载 JDBC 驱动程序。 因此，使用驱动程序 jar 库时，应用程序无需调用 `Class.forName` 方法来注册或加载驱动程序。  
  
当调用驱动程序管理器类的 getConnection 方法时，相应的驱动程序会从已注册的 JDBC 驱动程序集中找到。 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar 文件包括"META-INF/services/java.sql.Driver"文件，其中包含**com.microsoft.sqlserver.jdbc.SQLServerDriver**作为已注册的驱动程序。 当前通过使用 Class.forName 方法加载驱动程序的现有应用程序将继续工作，无需进行修改。  
  
> [!NOTE]  
> sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 类库无法用于较早版本的 Java Runtime Environment (JRE)。 请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)支持的 JRE 版本的列表[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。  

有关如何连接数据源和使用连接 URL 的详细信息，请参阅[创建连接 URL](../../connect/jdbc/building-the-connection-url.md)并[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另请参阅  

[JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
