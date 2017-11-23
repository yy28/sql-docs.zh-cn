---
title: "跟踪驱动程序操作 |Microsoft 文档"
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
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
caps.latest.revision: "42"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 717c1d05c666efef553a77d11dcd8105a0834832
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="tracing-driver-operation"></a>跟踪驱动程序操作
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持的跟踪 （或日志记录） 以帮助解决问题和使用 JDBC 驱动程序的问题，你的应用程序中使用时使用。 若要启用的跟踪，JDBC 驱动程序，请使用 java.util.logging，提供一组类，用于创建记录器和 LogRecord 对象中的日志记录 Api。  
  
> [!NOTE]  
>  对于 JDBC 驱动程序中包含的本地组件 (sqljdbc_xa.dll)，可通过内置诊断 (BID) 框架启用跟踪。 有关投标信息，请参阅[在 SQL Server 中进行数据访问跟踪](http://go.microsoft.com/fwlink/?LinkId=70042)。  
  
 当开发你的应用程序时，您可以对进行调用反过来创建 LogRecord 对象，然后传递给处理程序对象的处理的记录器对象。 记录器和处理程序对象都使用日志记录级别，并根据需要处理日志记录筛选器，以控制哪些 LogRecords。 日志记录操作完成后，处理程序对象 （可选） 可以使用格式化程序对象发布的日志信息。  
  
 默认情况下，java.util.logging 框架会将其输出写入到文件中。 该输出日志文件必须对 JDBC 驱动程序运行时所在的上下文具有写入权限。  
  
> [!NOTE]  
>  有关使用各种日志记录对象进行程序跟踪的详细信息，请参阅 Sun Microsystems 网站上的 Java Logging APIs（英文）文档。  
  
 以下各部分介绍了可记录的日志记录级别和类别，并提供了有关如何在应用程序中启用跟踪的信息。  
  
## <a name="logging-levels"></a>日志记录级别  
 创建的每条日志消息都有相关联的日志记录级别。 日志记录级别确定日志消息，由定义的重要性**级别**java.util.logging 中的类。 启用一个级别的日志记录还会启用所有较高级别的日志记录。 本节介绍公共日志记录类别和内部日志记录类别的日志记录级别。 有关日志记录类别的详细信息，请参阅本主题的“日志记录类别”部分。  
  
 下表逐一介绍了公共日志记录类别每个可用的日志记录级别。  
  
|Name|Description|  
|----------|-----------------|  
|SEVERE|表示严重故障，为最高日志记录级别。 在 JDBC 驱动程序中，该级别用于报告错误和异常。|  
|WARNING|指示潜在的问题。|  
|INFO|提供信息性消息。|  
|CONFIG|提供配置消息。 请注意，JDBC Driver 当前不提供任何配置消息。|  
|FINE|提供基本的跟踪信息，包括公共方法引发的所有异常。|  
|FINER|提供详细的跟踪信息，包括具有相关参数数据类型的所有公共方法的进入点和退出点，以及公共类的所有公共属性。 此外，输入参数、 输出参数和除 CLOB、 BLOB、 NCLOB、 读取器，方法返回值\<流 > 返回值类型。|  
|FINEST|提供非常详细的跟踪信息。 此为最低日志记录级别。|  
|OFF|关闭日志记录功能。|  
|ALL|启用所有消息的日志记录。|  
  
 下表逐一介绍了内部日志记录类别每个可用的日志记录级别。  
  
|Name|Description|  
|----------|-----------------|  
|SEVERE|表示严重故障，为最高日志记录级别。 在 JDBC 驱动程序中，该级别用于报告错误和异常。|  
|WARNING|指示潜在的问题。|  
|INFO|提供信息性消息。|  
|FINE|提供跟踪信息，包括基本的对象创建和析构。 此外，还包括公共方法引发的所有异常。|  
|FINER|提供详细的跟踪信息，包括具有相关参数数据类型的所有公共方法的进入点和退出点，以及公共类的所有公共属性。 此外，输入参数、 输出参数和除 CLOB、 BLOB、 NCLOB、 读取器，方法返回值\<流 > 返回值类型。<br /><br /> 以下日志记录类别版本 1.2 的 JDBC 驱动程序中存在，且必须正常的日志记录级别： [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)， [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)，XA，和[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). 从 2.0 发行版开始，这些日志记录类别升级到 FINER 级别。|  
|FINEST|提供非常详细的跟踪信息。 此为最低日志记录级别。<br /><br /> 下列日志记录类别存在于 JDBC Driver 1.2 中并具有 FINEST 日志记录级别：TDS.DATA 和 TDS.TOKEN。 从 2.0 发行版开始，这些日志记录类别保持 FINEST 日志记录级别。|  
|OFF|关闭日志记录功能。|  
|ALL|启用所有消息的日志记录。|  
  
## <a name="logging-categories"></a>日志记录类别  
 当创建记录器对象时，你必须告知对象的已命名的实体或你感兴趣获取从日志信息的类别。 JDBC Driver 支持下列公共日志记录类别，这些日志记录类别都是在 com.microsoft.sqlserver.jdbc 驱动程序包中定义的。  
  
|Name|Description|  
|----------|-----------------|  
|连接|将消息记录[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 应用程序可将日志记录级别设置为 FINER。|  
|。|将消息记录[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类。 应用程序可将日志记录级别设置为 FINER。|  
|DataSource|将消息记录[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
|ResultSet|将消息记录[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类。 应用程序可将日志记录级别设置为 FINER。|  
|驱动程序|将消息记录[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md)类。 应用程序可将日志记录级别设置为 FINER。|  
  
 从 Microsoft JDBC Driver 2.0 开始，JDBC Driver 还提供了 com.microsoft.sqlserver.jdbc.internals 包，后者包括对下列内部日志记录类别的日志记录支持。  
  
|Name|Description|  
|----------|-----------------|  
|AuthenticationJNI|有关 Windows 的日志消息集成身份验证问题 (时**authenticationScheme**连接属性隐式或显式设置为**NativeAuthentication**)。<br /><br /> 应用程序可将日志记录级别设置为 FINEST 和 FINE。|  
|的|将消息记录[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 应用程序可将日志记录级别设置为 FINE 和 FINER。|  
|SQLServerDataSource|将消息记录[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)， [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)，和[SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md)类。<br /><br /> 应用程序可将日志记录级别设置为 FINER。|  
|InputStream|记录有关下列数据类型的消息：java.io.InputStream、java.io.Reader 以及具有 max 说明符的数据类型（如 varchar、nvarchar 和 varbinary 数据类型）。<br /><br /> 应用程序可将日志记录级别设置为 FINER。|  
|SQLServerException|将消息记录[SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerResultSet|将消息记录[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类。 应用程序可将日志记录级别设置为 FINE、FINER 和 FINEST。|  
|SQLServerStatement|将消息记录[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类。 应用程序可将日志记录级别设置为 FINE、FINER 和 FINEST。|  
|XA|记录消息中的所有 XA 事务[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md)类。 应用程序可将日志记录级别设置为 FINE 和 FINER。|  
|KerbAuthentication|记录有关类型 4 Kerberos 身份验证的消息 (时**authenticationScheme**连接属性设置为**JavaKerberos**)。 应用程序可将日志记录级别设置为 FINE 或 FINER。|  
|TDS.DATA|记录包含驱动程序和 SQL Server 之间的 TDS 协议级别对话的消息。 发送和接收的每个 TDS 数据包的详细内容都以 ASCII 和十六进制格式记录。 不记录登录凭据（用户名和密码）。 但记录所有其他数据。<br /><br /> 该类别会创建非常冗长而详细的消息，并且只有通过将日志记录级别设置为 FINEST 才能启用它。|  
|TDS.Channel|该类别跟踪 SQL Server 对 TCP 通信通道的操作。 记录的消息包括套接字的打开和关闭以及读取和写入。 还跟踪与 SQL Server 建立安全套接字层 (SSL) 连接的相关消息。<br /><br /> 该类别只有通过将日志记录级别设置为 FINE、FINER 或 FINEST 才能启用。|  
|TDS.Writer|该类别跟踪对 TDS 信道的写入。 请注意，只跟踪写入的长度，不跟踪内容。 该类别还跟踪将关注信号发送给服务器以取消语句的执行时出现的问题。<br /><br /> 该类别只有通过将日志记录级别设置为 FINEST 才能启用。|  
|TDS.Reader|该类别跟踪 FINEST 级别 TDS 信道的某些读取操作。 在 FINEST 级别，跟踪可能非常详细。 在 WARNING 和 SEVERE 级别，该类别跟踪在驱动程序关闭连接之前，驱动程序何时从 SQL Server 收到无效的 TDS 协议。<br /><br /> 该类别只有通过将日志记录级别设置为 FINER 和 FINEST 才能启用。|  
|TDS.Command|此类别跟踪低级别的状态转换和其他与执行 TDS 命令，如关联信息[!INCLUDE[tsql](../../includes/tsql_md.md)]语句执行、 结果集游标提取、 提交，依次类推。<br /><br /> 该类别只有通过将日志记录级别设置为 FINEST 才能启用。|  
|TDS.TOKEN|该类别仅记录 TDS 包内的标记，不如 TDS.DATA 类别详细。 只能通过将日志记录级别设置为 FINEST 来启用它。<br /><br /> 在 FINEST 级别，当 TDS 标记在响应中进行处理时，此类别对其进行跟踪。 在 SEVERE 级别，该类别跟踪何时遇到无效的 TDS 标记。|  
|SQLServerDatabaseMetaData|将消息记录[SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerResultSetMetaData|将消息记录[SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerParameterMetaData|将消息记录[SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerBlob|将消息记录[SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerClob|将消息记录[SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerSQLXML|内部 SQLServerSQLXML 类中记录的消息。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerDriver|将消息记录[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
|SQLServerNClob|将消息记录[SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md)类。 应用程序可将日志记录级别设置为 FINE。|  
  
## <a name="enabling-tracing-programmatically"></a>以编程方式启用跟踪  
 可启用跟踪以编程方式通过创建记录器对象，并指示类别将被记录。 例如，以下代码显示了如何启用 SQL 语句的日志记录：  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 若要在代码中关闭日志记录，请使用以下代码：  
  
```  
logger.setLevel(Level.OFF);  
```  
  
 若要记录所有可用类别，请使用以下代码：  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 若要禁止记录某个特定类别，请使用以下代码：  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>使用 Logging.Properties 文件启用跟踪  
 您还可以通过启用跟踪`logging.properties`文件，可在`lib`你 Java Runtime Environment (JRE) 的安装目录。 该文件可用于设置记录程序和处理程序的默认值，在启用跟踪时会用到这些值。  
  
 以下是你可以在中进行的设置的示例`logging.properties`文件：  
  
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
>  你可以设置中的属性`logging.properties`使用属于 java.util.logging LogManager 对象的文件。  
  
## <a name="see-also"></a>另请参阅  
 [诊断与 JDBC 驱动程序有关的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
