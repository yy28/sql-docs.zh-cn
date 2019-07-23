---
title: 跟踪驱动程序操作 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8e04fe67605c97e12c688e0b05b8c437b6aa182
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916688"
---
# <a name="tracing-driver-operation"></a>跟踪驱动程序操作
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持使用跟踪（或日志记录）协助解决在应用程序中使用 JDBC 驱动程序时出现的问题。 若要启用跟踪，JDBC 驱动程序需要使用 java.util.logging 中的日志记录 API，java.util.logging 可提供用于创建 Logger 和 LogRecord 对象的类集。  
  
> [!NOTE]  
>  对于 JDBC 驱动程序中包含的本地组件 (sqljdbc_xa.dll)，可通过内置诊断 (BID) 框架启用跟踪。 有关 BID 的信息，请参阅 [SQL Server 中的数据访问跟踪](https://go.microsoft.com/fwlink/?LinkId=70042)。  
  
 开发应用程序时，可对 Logger 对象进行调用，它会转而创建 LogRecord 对象（这些对象随后会传递给 Handler 对象进行处理）。 记录器和处理程序对象均使用日志记录级别和记录筛选器 (可选) 来规定处理哪些 LogRecords。 完成日志记录操作后，Handler 对象可选择使用 Formatter 对象发布日志信息。  
  
 默认情况下，java.util.logging 框架会将其输出写入到文件中。 该输出日志文件必须对 JDBC 驱动程序运行时所在的上下文具有写入权限。  
  
> [!NOTE]  
>  有关使用各种日志记录对象进行程序跟踪的详细信息，请参阅 Sun Microsystems 网站上的 Java Logging APIs（英文）文档。  
  
 以下各部分介绍了可记录的日志记录级别和类别，并提供了有关如何在应用程序中启用跟踪的信息。  
  
## <a name="logging-levels"></a>日志记录级别  
 创建的每条日志消息都有相关联的日志记录级别。 日志记录级别决定了日志消息的重要性，该重要性由 java.util.logging 中的 Level 类定义  。 启用一个级别的日志记录还会启用所有较高级别的日志记录。 本节介绍公共日志记录类别和内部日志记录类别的日志记录级别。 有关日志记录类别的详细信息，请参阅本文的“日志记录类别”部分。  
  
 下表逐一介绍了公共日志记录类别每个可用的日志记录级别。  
  
|“属性”|描述|  
|----------|-----------------|  
|SEVERE|表示严重故障，为最高日志记录级别。 在 JDBC 驱动程序中，该级别用于报告错误和异常。|  
|WARNING|指示潜在的问题。|  
|INFO|提供信息性消息。|  
|CONFIG|提供配置消息。 请注意，JDBC 驱动程序当前不提供任何配置消息。|  
|FINE|提供基本的跟踪信息，包括公共方法引发的所有异常。|  
|FINER|提供详细的跟踪信息，包括具有相关参数数据类型的所有公共方法的进入点和退出点，以及公共类的所有公共属性。 此外，还包括输入参数、输出参数以及除 CLOB、BLOB、NCLOB、Reader 和 \<stream> 返回值类型以外的方法返回值。|  
|FINEST|提供非常详细的跟踪信息。 此为最低日志记录级别。|  
|OFF|关闭日志记录功能。|  
|ALL|启用所有消息的日志记录。|  
  
 下表逐一介绍了内部日志记录类别每个可用的日志记录级别。  
  
|“属性”|描述|  
|----------|-----------------|  
|SEVERE|表示严重故障，为最高日志记录级别。 在 JDBC 驱动程序中，该级别用于报告错误和异常。|  
|WARNING|指示潜在的问题。|  
|INFO|提供信息性消息。|  
|FINE|提供跟踪信息，包括基本的对象创建和析构。 此外，还包括公共方法引发的所有异常。|  
|FINER|提供详细的跟踪信息，包括具有相关参数数据类型的所有公共方法的进入点和退出点，以及公共类的所有公共属性。 此外，还包括输入参数、输出参数以及除 CLOB、BLOB、NCLOB、Reader 和 \<stream> 返回值类型以外的方法返回值。<br /><br /> 下列日志记录类别存在于 JDBC Driver 1.2 中并具有 FINE 日志记录级别：[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)、[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、XA 和 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)。 从 2.0 发行版开始，这些日志记录类别升级到 FINER 级别。|  
|FINEST|提供非常详细的跟踪信息。 此为最低日志记录级别。<br /><br /> 下列日志记录类别存在于 JDBC Driver 1.2 中并具有 FINEST 日志记录级别：TDS.DATA 和 TDS.TOKEN。 从 2.0 发行版开始，这些日志记录类别保持 FINEST 日志记录级别。|  
|OFF|关闭日志记录功能。|  
|ALL|启用所有消息的日志记录。|  
  
## <a name="logging-categories"></a>日志记录类别  
 创建 Logger 对象时，必须告知该对象你希望从中获取日志信息的命名实体或类别。 JDBC Driver 支持下列公共日志记录类别，这些日志记录类别都是在 com.microsoft.sqlserver.jdbc 驱动程序包中定义的。  
  
|“属性”|描述|  
|----------|-----------------|  
|连接|在 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINER。|  
|。|在 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINER。|  
|DataSource|在 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|ResultSet|在 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINER。|  
|驱动程序|在 [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINER。|  
  
 从 Microsoft JDBC Driver 2.0 开始，JDBC Driver 还提供了 com.microsoft.sqlserver.jdbc.internals 包，后者包括对下列内部日志记录类别的日志记录支持。  
  
|“属性”|描述|  
|----------|-----------------|  
|AuthenticationJNI|记录有关 Windows 集成身份验证问题的消息 ( **authenticationScheme**连接属性隐式或显式设置为**NativeAuthentication**)。<br /><br /> 应用程序可将日志记录级别设置为 FINEST 和 FINE。|  
|的|在 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE 和 FINER。|  
|SQLServerDataSource|在 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)、[SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 和 [SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 类中记录消息。<br /><br /> 应用程序可将日志记录级别设置为 FINER。|  
|InputStream|记录有关下列数据类型的消息：java.io.InputStream、java.io.Reader 以及具有 max 说明符的数据类型（如 varchar、nvarchar 和 varbinary 数据类型）。<br /><br /> 应用程序可将日志记录级别设置为 FINER。|  
|SQLServerException|在 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerResultSet|在 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE、FINER 和 FINEST。|  
|SQLServerStatement|在 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE、FINER 和 FINEST。|  
|XA|在 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 类中记录所有 XA 事务的日志消息。 应用程序可将日志记录级别设置为 FINE 和 FINER。|  
|KerbAuthentication|记录有关类型 4 Kerberos 身份验证的消息 ( **authenticationScheme**连接属性设置为**JavaKerberos**)。 应用程序可将日志记录级别设置为 FINE 或 FINER。|  
|TDS.DATA|记录包含驱动程序和 SQL Server 之间的 TDS 协议级别对话的消息。 发送和接收的每个 TDS 数据包的详细内容都以 ASCII 和十六进制格式记录。 不记录登录凭据（用户名和密码）。 但记录所有其他数据。<br /><br /> 该类别会创建非常冗长而详细的消息，并且只有通过将日志记录级别设置为 FINEST 才能启用它。|  
|TDS.Channel|该类别跟踪 SQL Server 对 TCP 通信通道的操作。 记录的消息包括套接字的打开和关闭以及读取和写入。 还跟踪与 SQL Server 建立安全套接字层 (SSL) 连接的相关消息。<br /><br /> 该类别只有通过将日志记录级别设置为 FINE、FINER 或 FINEST 才能启用。|  
|TDS.Writer|该类别跟踪对 TDS 信道的写入。 请注意，只跟踪写入的长度，不跟踪内容。 该类别还跟踪将关注信号发送给服务器以取消语句的执行时出现的问题。<br /><br /> 该类别只有通过将日志记录级别设置为 FINEST 才能启用。|  
|TDS.Reader|该类别跟踪 FINEST 级别 TDS 信道的某些读取操作。 在 FINEST 级别，跟踪可能非常详细。 在 WARNING 和 SEVERE 级别，该类别跟踪在驱动程序关闭连接之前，驱动程序何时从 SQL Server 收到无效的 TDS 协议。<br /><br /> 该类别只有通过将日志记录级别设置为 FINER 和 FINEST 才能启用。|  
|TDS.Command|该类别跟踪低级状态转换以及与执行 TDS 命令（例如 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句执行、ResultSet 游标获取、提交等）关联的其他信息。<br /><br /> 该类别只有通过将日志记录级别设置为 FINEST 才能启用。|  
|TDS.TOKEN|该类别仅记录 TDS 包内的标记，不如 TDS.DATA 类别详细。 它只有通过将日志记录级别设置为 FINEST 才能启用。<br /><br /> 在 FINEST 级别，当 TDS 标记在响应中进行处理时，此类别对其进行跟踪。 在 SEVERE 级别，该类别跟踪何时遇到无效的 TDS 标记。|  
|SQLServerDatabaseMetaData|在 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerResultSetMetaData|在 [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerParameterMetaData|在 [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerBlob|在 [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerClob|在 [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerSQLXML|在内部 SQLServerSQLXML 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerDriver|在 [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerNClob|在 [SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md) 类中记录消息。 应用程序可将日志记录级别设置为 FINE。|  
  
## <a name="enabling-tracing-programmatically"></a>以编程方式启用跟踪  
 通过创建 Logger 对象并指示记录类别，可以编程方式启用跟踪。 例如，以下代码显示了如何启用 SQL 语句的日志记录：  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 若要在代码中关闭日志记录，请使用以下代码：  
  
```java
logger.setLevel(Level.OFF);  
```  
  
 若要记录所有可用类别，请使用以下代码：  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 若要禁止记录某个特定类别，请使用以下代码：  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>使用 Logging.Properties 文件启用跟踪  
 还可以使用 `logging.properties` 文件来启用跟踪，该文件可在 Java Runtime Environment (JRE) 安装文件的 `lib` 目录中找到。 该文件可用于设置记录程序和处理程序的默认值，在启用跟踪时会用到这些值。  
  
 以下是可在 `logging.properties` 文件中进行的设置的示例：  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  使用 java.util.logging 中的 LogManager 对象可设置 `logging.properties` 文件中的属性。  
  
## <a name="see-also"></a>另请参阅  
 [诊断与 JDBC 驱动程序有关的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
