---
title: 使用 JDBC 驱动程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03ea3e895fb7d70b392e0c25372536770308049d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-jdbc-driver"></a>使用 JDBC 驱动程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本部分提供有关进行简单连接到的快速入门说明[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用数据库[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。 连接到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]首先必须安装在本地计算机或服务器，并且必须在本地计算机上安装的 JDBC 驱动程序。  
  
## <a name="choosing-the-right-jar-file"></a>选择正确的 JAR 文件  
 SQL Server 的 Microsoft JDBC 驱动程序 6.4 提供**mssql jdbc 6.4.0.jre7.jar**， **mssql jdbc 6.4.0.jre8.jar**，和**mssql jdbc 6.4.0.jre9.jar**类库具体取决于你首选的 Java Runtime Environment (JRE) 设置要使用的文件。  
 
 SQL Server 的 Microsoft JDBC 驱动程序 6.2 提供**mssql jdbc 6.2.1.jre7.jar**，和**mssql jdbc 6.2.1.jre8.jar**类库文件，具体取决于你首选的 Java 运行时使用环境 (JRE) 设置。  
  
  Microsoft JDBC 驱动程序 6.0 和 4.2 for SQL Server 提供**sqljdbc41.jar**，和**sqljdbc42.jar**类具体取决于你首选的 Java Runtime Environment (JRE) 设置要使用的库文件。  
  
 SQL Server 的 Microsoft JDBC Driver 4.1 提供**sqljdbc41.jar**类库文件，具体取决于你首选的 Java Runtime Environment (JRE) 设置中使用。  
    
 你的选择还将确定可用功能。 有关要选择的 JAR 文件的详细信息，请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="setting-the-classpath"></a>设置 Classpath  
 JDBC 驱动程序并未包含在 Java SDK 中。 如果你想要使用它，则必须设置类路径来包括**sqljdbc.jar**文件， **sqljdbc4.jar**文件， **sqljdbc41.jar**文件，或**sqljdbc42.jar**文件。 如果使用 JDBC 驱动程序 6.2 设置类路径来包括**mssql jdbc 6.2.1.jre7.jar**或**mssql jdbc 6.2.1.jre8.jar**。 如果使用 JDBC 驱动程序 6.4、 设置类路径来包括**mssql jdbc 6.4.0.jre7.jar**， **mssql jdbc 6.4.0.jre8.jar**或**mssql jdbc 6.4.0.jre9.jar**。 如果类路径缺少条目，你的应用程序将引发常见的“找不到类”异常。  
  
### <a name="for-microsoft-jdbc-driver-64"></a>For Microsoft JDBC Driver 6.4
 **Mssql jdbc 6.4.0.jre7.jar**， **mssql jdbc 6.4.0.jre8.jar**或**mssql jdbc 6.4.0.jre9.jar**文件安装在以下位置：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \mssql-jdbc-6.4.0.jre7.jar 
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \mssql-jdbc-6.4.0.jre8.jar
 
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \mssql-jdbc-6.4.0.jre9.jar
  
 下面是用于 Windows 应用程序的 CLASSPATH 语句示例：  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
 下面是用于 Unix/Linux 应用程序的 CLASSPATH 语句示例：  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
 你必须确保 CLASSPATH 语句包含只有一个[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，如 mssql jdbc 6.4.0.jre7.jar、 mssql jdbc 6.4.0.jre8.jar 或 mssql jdbc 6.4.0.jre9.jar。   

### <a name="for-microsoft-jdbc-driver-62"></a>For Microsoft JDBC Driver 6.2
 **Mssql jdbc 6.2.1.jre7.jar**或**mssql jdbc 6.2.1.jre8.jar**文件安装在以下位置：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \mssql-jdbc-6.2.1.jre7.jar 
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \mssql-jdbc-6.2.1.jre8.jar
  
 下面是用于 Windows 应用程序的 CLASSPATH 语句示例：  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.1.jre8.jar`  
  
 下面是用于 Unix/Linux 应用程序的 CLASSPATH 语句示例：  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.1.jre8.jar`  
  
 你必须确保 CLASSPATH 语句包含只有一个[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，如 mssql jdbc 6.2.1.jre7.jar 或 mssql jdbc 6.2.1.jre8.jar。  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>有关 Microsoft JDBC Driver 4.1、 4.2 和 6.0
 Sqljdbc.jar 文件、sqljdbc4.jar 文件、sqljdbc41.jar 或 sqljdbc42.jar 文件安装在以下位置：  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \sqljdbc.jar  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \sqljdbc4.jar  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \sqljdbc41.jar  
  
 \<*安装目录*> \sqljdbc_\<*版本*>\\<*语言*> \sqljdbc42.jar  
  
 下面是用于 Windows 应用程序的 CLASSPATH 语句示例：  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
 下面是用于 Unix/Linux 应用程序的 CLASSPATH 语句示例：  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
 你必须确保 CLASSPATH 语句包含只有一个[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，如 sqljdbc.jar、 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar。  
  
> [!NOTE]  
>  在 Windows 系统上，长度超过 8.3 文件名约定的目录名称或带有空格的文件夹名称可能会导致类路径问题。 如果你怀疑这些类型的问题，应暂时将移 sqljdbc.jar、 sqljdbc4.jar 文件或 sqljdbc41.jar 文件到简单的目录名称如`C:\Temp`、 更改的类路径，以及确定是否，以解决问题。  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>直接在命令提示符运行的应用程序  
 classpath 是在操作系统中配置的。 将 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 追加到系统的 classpath 中。 或者，可以通过使用运行应用程序在 Java 命令行上指定的类路径`java -classpath`选项。  
  
### <a name="applications-that-run-in-an-ide"></a>在 IDE 中运行的应用程序  
 每个 IDE 供应商都提供了在 IDE 中设置 classpath 的不同方法。 仅在操作系统中设置 classpath 将无法正常工作。 必须将 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 添加到 IDE 类路径。  
  
### <a name="servlets-and-jsps"></a>Servlet 和 JSP  
 Servlet 和 JSP 在 servlet/JSP 引擎（如 Tomcat）中运行。 必须根据 servlet/JSP 引擎文档来设置 classpath。 仅在操作系统中设置 classpath 将无法正常工作。 一些 servlet/JSP 引擎提供了设置屏幕，用于设置引擎的 classpath。 在这种情况下，必须将正确的 JDBC 驱动程序 JAR 文件追加到现有的引擎 classpath，然后重新启动引擎。 在其他情况下，通过在引擎安装期间将 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 复制到 lib 之类的特定目录，可以部署此驱动程序。 也可以在引擎专用的配置文件中指定引擎驱动程序的 classpath。  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  
 Enterprise Java Bean (EJB) 在 EJB 容器中运行。 EJB 容器来自多家供应商。 Java 小程序在浏览器中运行，但是从 Web 服务器上下载的。 复制到 web 服务器根的 sqljdbc.jar、 sqljdbc4.jar、 sqljdbc41.jar 和指定 JAR 文件的名称在 HTML 存档选项卡中的小程序，例如， `<applet ... archive=sqljdbc.jar>`。  
  
## <a name="making-a-simple-connection-to-a-database"></a>与数据库建立简单连接  
 使用 sqljdbc.jar 类库时，应用程序必须首先按如下所示注册驱动程序：  
  
 `Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  
  
 加载驱动程序后，你可以通过使用连接 URL 和驱动程序管理器类的 getConnection 方法来建立连接：  
  
```  
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 在 JDBC API 4.0、 增强 DriverManager.getConnection 方法以自动加载 JDBC 驱动程序。 因此，应用程序不需要调用 Class.forName 方法以注册或使用 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar 类库时加载的驱动程序。  
  
 当调用驱动程序管理器类的 getConnection 方法时，合适的驱动程序位于从已注册的 JDBC 驱动程序集。 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar 文件包括"META-INF/services/java.sql.Driver"文件，其中包含**com.microsoft.sqlserver.jdbc.SQLServerDriver**作为已注册的驱动程序。 现有应用程序，通过使用 Class.forName 方法当前加载的驱动程序，将继续无需修改即可。  
  
> [!NOTE]  
>  sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 类库无法用于较早版本的 Java Runtime Environment (JRE)。 请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)有关支持的 JRE 版本的列表[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。  
  
 有关如何与数据源连接和使用连接 URL 的详细信息，请参阅[生成连接 URL](../../connect/jdbc/building-the-connection-url.md)和[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
