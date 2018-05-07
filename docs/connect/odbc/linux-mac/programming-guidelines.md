---
title: 编程指南 (ODBC Driver for SQL Server) |Microsoft 文档
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68a7b720ab2ab9a4280cc6d8a22a37cf0cad0f5d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="programming-guidelines"></a>编程指南

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

编程功能[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 macOS 和 Linux 上基于在 ODBC[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]本机客户端 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151))。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 本机客户端将基于 Windows 数据访问组件中的 ODBC ([ODBC 程序员参考](http://go.microsoft.com/fwlink/?LinkID=45250))。  

ODBC 应用程序可以使用多个活动结果集 (MARS) 和其他[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]特定功能包括`/usr/local/include/msodbcsql.h`后的 unixODBC 标头 (`sql.h`， `sqlext.h`， `sqltypes.h`，和`sqlucode.h`)。 然后，使用的相同符号名称[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-你将在你 Windows ODBC 应用程序的特定项。

## <a name="available-features"></a>可用功能  
以下各节从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]适用于 ODBC 的本机客户端文档 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) 时在 macOS 和 Linux 上使用的 ODBC 驱动程序都有效：  

-   [与 SQL Server 通信 (ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [连接和查询的超时支持](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [游标](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [日期/时间改进 (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [执行查询 (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [处理错误和消息](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Kerberos 身份验证](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [大型 CLR 用户定义类型 (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [（除外分布式事务） 中执行事务 (ODBC)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [处理结果 (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [运行存储过程](http://msdn.microsoft.com/library/ms131440.aspx)
-   [稀疏列支持 (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 加密](http://msdn.microsoft.com/library/ms131691.aspx)
-   [表值的参数](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [Utf-8 和 utf-16 命令和数据的 api](http://msdn.microsoft.com/library/ff878241.aspx)
-   [使用目录函数](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>不支持的功能

以下功能不验证在 macOS 和 Linux 上的 ODBC 驱动程序的此版本中正常工作：

-   故障转移群集连接
-   [透明网络 IP 解析](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution)（之前 ODBC 驱动程序 17）
-   [高级驱动程序跟踪](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

不在 macOS 和 Linux 上的 ODBC 驱动程序的此版本中提供以下功能： 

-   分布式事务 （不支持 SQL_ATTR_ENLIST_IN_DTC 属性）  
-   数据库镜像  
-   FILESTREAM  
-   分析 ODBC 驱动程序性能中, 所述[SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099)，以及下列与性能相关的连接属性：  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   C 间隔类型，如 SQL_C_INTERVAL_YEAR_TO_MONTH (记录在[数据类型标识符和描述符](http://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   SQLSetConnectAttr 函数 SQL_ATTR_ODBC_CURSORS 属性 SQL_CUR_USE_ODBC 值。

## <a name="character-set-support"></a>字符集支持

对于 ODBC Driver 13 和 13.1，SQLCHAR 数据必须是 utf-8。 不支持任何其他编码。

对于 ODBC 驱动程序 17 支持 SQLCHAR 之一中的以下字符集/编码的数据：

|名称|Description|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS Latin 美国|
|CP850|MS-DOS 拉丁文 1|
|CP874|Latin/泰语|
|CP932|日语，Shift JIS|
|CP936|简体中文 GBK|
|CP949|朝鲜语，EUC KR|
|CP950|繁体中文 Big5|
|CP1251|西里尔语|
|CP1253|希腊语|
|CP1256|阿拉伯语|
|CP1257|波罗的语|
|CP1258|越南语|
|ISO-8859-1 / CP1252|Latin 1|
|ISO-8859-2 / CP1250|Latin 2|
|ISO-8859-3|Latin 3|
|ISO-8859-4|Latin-4|
|ISO-8859-5|拉丁/西里尔|
|ISO-8859-6|Latin/阿拉伯语|
|ISO-8859-7|拉丁语/希腊语|
|ISO-8859-8 / CP1255|希伯来语|
|ISO-8859-9 / CP1254|土耳其语|
|ISO-8859-13|Latin 7|
|ISO-8859-15|拉丁语 9|

在连接时该驱动程序检测到的进程中加载的当前区域设置。 如果它使用上面的编码之一，驱动程序使用 SQLCHAR （窄字符） 数据; 该编码否则，它默认为 utf-8。 由于所有进程启动的"C"区域设置中，默认情况下 （并因此导致为 utf-8 的驱动程序添加到默认），如果应用程序需要使用上面的编码之一，它应使用**setlocale**函数适当之前设置的区域设置连接;通过显式指定所需的区域设置或使用空字符串，例如`setlocale(LC_ALL, "")`使用环境的区域设置。

因此，在典型 Linux 或 Mac 环境中其中编码为 utf-8，ODBC 驱动程序 17 从 13 或 13.1 升级的用户将不会看到任何差异。 但是，应用程序使用通过上面的列表中的非 utf-8 编码`setlocale()`需要使用向/从驱动程序而不是 utf-8 数据该编码。

SQLWCHAR 数据必须是 UTF-16LE (Little Endian)。

当绑定使用 SQLBindParameter，输入的参数时如果窄字符 SQL 类型，如指定 SQL_VARCHAR，驱动程序将提供的数据转换从客户端为默认值 （通常代码页 1252年） 编码[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]编码。 对于输出参数，该驱动程序将从与向客户端编码的数据关联的排序规则信息中指定的编码转换。 但是，可能会丢失数据-编码中的字符源无法在目标编码中表示会将转换为一个问号 ('？ ')。

若要避免这种数据丢失，绑定输入的参数时，指定一个 Unicode SQL 字符类型，例如 SQL_NVARCHAR。 在这种情况下，该驱动程序将从客户端编码为 utf-16，可以表示所有 Unicode 字符转换。 此外，目标列或服务器上的参数还必须是 Unicode 类型 (**nchar**， **nvarchar**， **ntext**) 或另一个使用排序规则/编码，这可以表示原始的源数据的所有字符。 为避免数据丢失与 output 参数，指定是 Unicode SQL 类型和一个 Unicode C 类型 (SQL_C_WCHAR)，导致驱动程序 utf-16; 的形式返回数据或窄的 C 类型，并确保客户端编码可以表示源数据 （这是始终可能使用 utf-8。） 的所有字符

有关排序规则和编码的详细信息，请参阅[Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)。

有一些编码转换差异 Windows 和 Linux 和 macOS 上的 iconv 库的多个版本。 在代码页 1255年的文本数据 （希伯来语） 具有一个码位 (0xCA)，在转换为 Unicode 时的行为方式不同。 在 Windows 上，此字符将转换为 0x05BA utf-16 码位。 在 macOS 和使用早于 1.15 libiconv 版本的 Linux 上，它将转换为 0x00CA。 在与 iconv 库不支持的 Big5/CP950 2003 版本的 Linux 上 (名为`BIG5-2003`)，添加与该修订版本的字符将不会正确转换。 在代码页 932 （日语，Shift JIS），最初未定义编码标准中的字符进行解码的结果也不同。 例如，字节 0x80 在 Windows 上将转换为 U + 0080，但可能会变得 U + 30FB 在 Linux 和 macOS，具体取决于 iconv 版本上。

在 ODBC Driver 13 和 13.1 中，当 utf-8 多字节字符或 utf-16 代理项分布 SQLPutData 缓冲区，它导致数据损坏。 使用用于流式传输不会在部分字符编码中结束的 SQLPutData 的缓冲区。 使用 ODBC 驱动程序 17，已取消此限制。

## <a name="additional-notes"></a>其他说明  

1.  你可以建立专用的管理员连接 (DAC) 使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]身份验证和**托管，端口**。 首先，Sysadmin 角色成员需要发现 DAC 端口。 请参阅[用于数据库管理员的诊断连接](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port)若要了解如何。 例如，如果 DAC 端口 33000，你无法连接到其与`sqlcmd`，如下所示：  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 连接都必须使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]身份验证。  
    
2.  当所有语句属性均通过 SQLSetConnectAttr 传递时，UnixODBC 驱动程序管理器会为其返回“属性/选项标识符无效”。 在 Windows 上，当 SQLSetConnectAttr 收到语句属性值，它将导致驱动程序连接句柄的子级的所有活动语句上设置该值。  

## <a name="see-also"></a>另请参阅  
[常见问题](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[此版本驱动程序中的已知问题](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes.md)
