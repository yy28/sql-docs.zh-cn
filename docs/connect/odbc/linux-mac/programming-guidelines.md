---
title: 编程指南 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2edaeee9d073cb0c12a509bd23e3db9edf4b3894
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602182"
---
# <a name="programming-guidelines"></a>编程指南

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 和 Linux 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的编程功能建立在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)) 的基础之上。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 建立在 Windows 数据访问组件中的 ODBC（[ODBC 程序员参考](https://go.microsoft.com/fwlink/?LinkID=45250)）的基础之上。  

ODBC 应用程序可以使用多个活动结果集 (MARS) 和其他[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]通过包括的特定功能`/usr/local/include/msodbcsql.h`unixODBC 标头后 (`sql.h`， `sqlext.h`， `sqltypes.h`，并`sqlucode.h`)。 然后，使用与在 Windows ODBC 应用程序中将使用的相同的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 特定项符号名称。

## <a name="available-features"></a>可用功能  
在使用 macOS 和 Linux 上的 ODBC 驱动程序时，用于 ODBC ([ SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)) 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 文档的以下各个部分均有效：  

-   [与 SQL Server 通信 (ODBC)](https://msdn.microsoft.com/library/ms131692.aspx)  
-   [连接和查询超时支持](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
-   [游标](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
-   [日期/时间的改进 (ODBC)](https://msdn.microsoft.com/library/bb677319.aspx)  
-   [执行查询 (ODBC)](https://msdn.microsoft.com/library/ms131677.aspx)  
-   [处理错误和消息](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
-   [Kerberos 身份验证](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
-   [大型 CLR 用户定义类型 (ODBC)](https://msdn.microsoft.com/library/bb677316.aspx)  
-   [执行事务 (ODBC)（分布式事务除外）](https://msdn.microsoft.com/library/ms131706.aspx)  
-   [处理结果 (ODBC)](https://msdn.microsoft.com/library/ms130812.aspx)  
-   [运行存储过程](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)
-   [稀疏列支持 (ODBC)](https://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 加密](../../../relational-databases/native-client/features/using-encryption-without-validation.md)
-   [表值参数](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [用于命令和数据 API 的 UTF-8 和 UTF-16](https://msdn.microsoft.com/library/ff878241.aspx)
-   [使用目录函数](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  

## <a name="unsupported-features"></a>不支持的功能

以下功能不验证在 macOS 和 Linux 上在此版本的 ODBC 驱动程序中正常工作：

-   故障转移群集连接
-   [透明网络 IP 解析](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution)（之前 ODBC 驱动程序 17）
-   [高级驱动程序跟踪](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

以下功能在此版本的 macOS 和 Linux 上的 ODBC 驱动程序中不可用： 

-   分布式事务（不支持 SQL_ATTR_ENLIST_IN_DTC 属性）  
-   数据库镜像  
-   FILESTREAM  
-   在 [SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=234099) 中讨论了 ODBC 驱动程序性能事件分析，以及以下与性能相关的连接属性：  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   诸如 SQL_C_INTERVAL_YEAR_TO_MONTH（记录在[数据类型标识符和描述符](https://msdn.microsoft.com/library/ms716351(VS.85).aspx)中）的 C 间隔类型
-   SQLSetConnectAttr 函数的 SQL_ATTR_ODBC_CURSORS 属性的 SQL_CUR_USE_ODBC 值。

## <a name="character-set-support"></a>字符集支持

有关 ODBC Driver 13 和 13.1，SQLCHAR 数据必须是 utf-8。 不支持任何其他编码。

对于 ODBC Driver 17，支持以下字符集/编码之一中的 SQLCHAR 数据：

|“属性”|描述|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS 拉丁语美国|
|CP850|MS-DOS 拉丁语 1|
|CP874|拉丁语/泰语|
|CP932|日语 (Shift_JIS)|
|CP936|简体中文 (GBK)|
|CP949|韩语 (EUC-KR)|
|CP950|繁体中文 (Big5)|
|CP1251|西里尔语|
|CP1253|希腊语|
|CP1256|阿拉伯语|
|CP1257|波罗的语|
|CP1258|越南语|
|ISO-8859-1 / CP1252|拉丁语-1|
|ISO-8859-2 / CP1250|拉丁语-2|
|ISO-8859-3|拉丁语-3|
|ISO-8859-4|拉丁语-4|
|ISO-8859-5|拉丁/西里尔|
|ISO-8859-6|拉丁语/阿拉伯语|
|ISO-8859-7|拉丁语/希腊语|
|ISO-8859-8 / CP1255|希伯来语|
|ISO-8859-9 / CP1254|土耳其语|
|ISO-8859-13|拉丁语-7|
|ISO-8859-15|拉丁语 9|

连接后，驱动程序检测到进程中加载的当前区域的设置。 如果发布使用上述编码之一，则驱动程序使用 SQLCHAR （窄字符） 数据; 该编码否则，它默认为 utf-8。 由于所有进程，在"C"区域设置中默认情况下启动 （并且因此导致驱动程序添加到默认为 utf-8），如果应用程序需要使用上述编码之一，则应使用**setlocale**函数之前适当地设置的区域设置连接;不论是通过显式指定所需的区域设置或使用空字符串，例如`setlocale(LC_ALL, "")`使用环境的区域设置。

因此，在典型 Linux 或 Mac 环境中，编码为 utf-8，ODBC Driver 17 从 13 或 13.1 升级的用户将不遵循任何差异。 但是，应用程序，使用上面的列表中通过一种非 utf-8 编码`setlocale()`需要使用该数据向/从驱动程序而不是 utf-8 编码。

SQLWCHAR 数据必须是 UTF-16LE (Little Endian)。

该驱动程序时如果窄字符 SQL 类型，例如 SQL_VARCHAR 指定绑定 SQLBindParameter，使用输入的参数，将从客户端编码为默认值 （通常代码页 1252年） 转换所提供的数据[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]编码。 对于输出参数，驱动程序将从客户端编码的数据与关联的排序规则信息中指定的编码转换。 但是，可能会丢失数据-中的字符的源编码无法在目标编码中表示会将转换为一个问号 (？)。

若要避免此数据丢失，绑定输入的参数时，指定 Unicode SQL 字符类型，例如 SQL_NVARCHAR。 在这种情况下，该驱动程序将从客户端编码为 utf-16，可以表示所有 Unicode 字符转换。 此外，在服务器上的参数的目标列必须也是 Unicode 类型 (**nchar**， **nvarchar**， **ntext**) 或另一个排序规则/编码，可以使用表示原始源数据的所有的字符。 为避免数据丢失与 output 参数，指定 Unicode SQL 类型和任一 Unicode C 类型 (SQL_C_WCHAR)，从而导致驱动程序以 utf-16; 形式返回数据或窄的 C 类型，并确保客户端编码可以表示源数据 （这是始终使用 utf-8。） 的所有字符

有关排序规则和编码的详细信息，请参阅[排序规则和 Unicode 支持](../../../relational-databases/collations/collation-and-unicode-support.md)。

有 Windows 和几个版本的 Linux 和 macOS 上的 iconv 库之间的一些编码转换差异。 在代码页 1255年中的文本数据 （希伯来语） 有一个码 (位 0xCA) 在转换为 Unicode 时具有不同的行为。 在 Windows 中，此字符将转换为 0x05BA 的 utf-16 码位。 在 macOS 和 Linux 与 libiconv 版本早于 1.15，它将转换为 0x00CA。 Linux 上的 iconv 库不支持 Big5/CP950 2003年修订版本的使用 (名为`BIG5-2003`)，使用该版本添加字符将不会正确转换。 在代码页 932 日语 (SHIFT-JIS） 集中，解码的字符编码标准中最初未定义的结果也不同。 例如，字节 0x80 在 Windows 上将转换为 U + 0080，但可能会变得 U + 30FB Linux 和 macOS，具体取决于 iconv 版本上。

在 ODBC 驱动程序 13 和 13.1 中，当在 SQLPutData 缓冲区上拆分 UTF-8 多字节字符或 UTF-16 代理项时，这会导致数据损坏。 使用用于流式传输不会在部分字符编码中结束的 SQLPutData 的缓冲区。 使用 ODBC Driver 17 消除这一限制。

## <a name="additional-notes"></a>其他说明  

1.  可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证和 主机,端口建立专用管理员连接 (DAC)。 首先，Sysadmin 角色成员需要发现 DAC 端口。 请参阅[用于数据库管理员的诊断连接](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port)来发现如何。 例如，如果 DAC 端口为 33000，可以使用 `sqlcmd` 连接它，如下所示：  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 连接必须使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证。  
    
2.  当所有语句属性均通过 SQLSetConnectAttr 传递时，UnixODBC 驱动程序管理器会为其返回“属性/选项标识符无效”。 在 Windows 上，当 SQLSetConnectAttr 接收某个语句属性值时，它会使驱动程序在属于连接句柄子级的所有活动语句上设置该值。  

## <a name="see-also"></a>另请参阅  
[常见问题解答](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[此版本驱动程序中的已知问题](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes.md)
