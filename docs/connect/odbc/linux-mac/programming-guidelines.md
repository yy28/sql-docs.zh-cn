---
title: 编程指南 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/12/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 591c0cc47a4f807172cbfd24b91f465144faae09
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042366"
---
# <a name="programming-guidelines"></a>编程指南

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 和 Linux 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的编程功能建立在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)) 的基础之上。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 建立在 Windows 数据访问组件中的 ODBC（[ODBC 程序员参考](https://go.microsoft.com/fwlink/?LinkID=45250)）的基础之上。  

通过在包含 unixODBC 标头（`sql.h`、`sqlext.h`、`sqltypes.h` 和 `sqlucode.h`）后包含 `/usr/local/include/msodbcsql.h`，ODBC 应用程序可以使用多重活动结果集 (MARS) 和其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 特定功能。 然后，使用与在 Windows ODBC 应用程序中将使用的相同的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 特定项符号名称。

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

尚未验证以下功能是否能在此版本的 macOS 和 Linux 上的 ODBC 驱动程序中正常使用：

-   故障转移群集连接
-   [透明网络 IP 解析](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution)（低于 ODBC Driver 17 版本）
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

对于 ODBC Driver 13 和 13.1，SQLCHAR 数据必须采用 UTF-8 编码。 不支持其他编码。

对于 ODBC Driver 17，支持以下一种字符集/编码中的 SQLCHAR 数据：

|“属性”|描述|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS 拉丁语(美国)|
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
|ISO-8859-1 / CP1252|拉丁语 - 1|
|ISO-8859-2 / CP1250|拉丁语 - 2|
|ISO-8859-3|拉丁语 - 3|
|ISO-8859-4|拉丁语 - 4|
|ISO-8859-5|拉丁语/西里尔语|
|ISO-8859-6|拉丁语/阿拉伯语|
|ISO-8859-7|拉丁语/希腊语|
|ISO-8859-8 / CP1255|希伯来语|
|ISO-8859-9 / CP1254|土耳其语|
|ISO-8859-13|拉丁语 - 7|
|ISO-8859-15|拉丁语 - 9|

连接后，驱动程序将检测加载它的进程的当前区域设置。 如果驱动程序使用上述一种编码，则驱动程序会将该编码用于 SQLCHAR（窄字符）数据；否则，默认使用 UTF-8。 默认情况下，由于所有进程都在“C”区域设置中启动（并因此导致驱动程序默认为 UTF-8），如果应用程序需要使用上述一种编码，则它应在连接前使用 setlocale 函数设置适当的区域设置：可显式指定所需的区域设置，或通过使用空字符串（例如，`setlocale(LC_ALL, "")`）来使用环境的区域设置。

因此，在编码为 UTF-8 的典型 Linux 或 Mac 环境中，从 ODBC Driver 13 或 13.1 升级的 ODBC Driver 17 用户将不会察觉到任何差异。 但是，通过 `setlocale()` 使用上述列表中非 UTF-8 编码的应用程序需要对传入/传出驱动程序的数据使用该编码，而不是 UTF-8。

SQLWCHAR 数据必须是 UTF-16LE (Little Endian)。

使用 SQLBindParameter 绑定输入参数时，如果指定了 SQL_VARCHAR 等窄字符 SQL 类型，则驱动程序会将提供的数据从客户端编码转换为默认（通常为代码页 1252）[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 编码。 对于输出参数，驱动程序将从与数据关联的排序规则信息中指定的编码转换为客户端编码。 但是，数据可能会丢失 - 无法以目标编码表示的源编码字符将转换为问号（“?”）。

要在绑定输入参数时避免此类数据丢失，请指定一种 Unicode SQL 字符类型，例如 SQL_NVARCHAR。 在这种情况下，驱动程序将从客户端编码转换为 UTF-16，该编码可表示所有 Unicode 字符。 此外，服务器上的目标列或参数也必须是 Unicode 类型（nchar、nvarchar 和 ntext）或带有排序规则/编码的其他类型，这可以表示原始源数据的所有字符。 为避免输出参数丢失数据，请指定 Unicode SQL 类型和 Unicode C 类型 (SQL_C_WCHAR)（使驱动程序以 UTF-16 形式返回数据）或窄 C 类型，并确保客户端编码可以表示源数据的所有字符（可始终使用 UTF-8 实现这一目的）。

有关排序规则和编码的详细信息，请参阅[排序规则和 Unicode 支持](../../../relational-databases/collations/collation-and-unicode-support.md)。

Windows 与 Linux 和 macOS 上的几个版本的 iconv 库之间存在一些编码转换差异。 代码页 1255（希伯来语）中的文本数据有一个码位 (0xCA) 在转换为 Unicode 时具有不同的行为。 在 Windows 中，此字符转换为 0x05BA 的 UTF-16 码位。 在具有 1.15 版本以前的 libiconv 的 macOS 和 Linux 上，它转换为 0x00CA。 在 iconv 库不支持 Big5/CP950 的 2003 修订（名为 `BIG5-2003`）的 Linux 上，使用该修订添加的字符将无法正确转换。 在代码页 932（日语(Shift-JIS)）中，最初未在编码标准中定义的字符的解码结果也存在差异。 例如，字节 0x80 在 Windows 上转换为 U+0080，但在 Linux 和 macOS 上可能会变为 U+30FB，具体取决于 iconv 版本。

在 ODBC 驱动程序 13 和 13.1 中，当在 SQLPutData 缓冲区上拆分 UTF-8 多字节字符或 UTF-16 代理项时，这会导致数据损坏。 使用用于流式传输不会在部分字符编码中结束的 SQLPutData 的缓冲区。 ODBC Driver 17 消除了这一限制。

## <a name="additional-notes"></a>其他说明  

1.  可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证和 主机,端口建立专用管理员连接 (DAC)。 首先，Sysadmin 角色成员需要发现 DAC 端口。 请参阅[用于数据库管理员的诊断连接](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port)来了解如何操作。 例如，如果 DAC 端口为 33000，可以使用 `sqlcmd` 连接它，如下所示：  

    ```
    sqlcmd -U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 连接必须使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证。  
    
2.  当所有语句属性均通过 SQLSetConnectAttr 传递时，UnixODBC 驱动程序管理器会为其返回“属性/选项标识符无效”。 在 Windows 上，当 SQLSetConnectAttr 接收某个语句属性值时，它会使驱动程序在属于连接句柄子级的所有活动语句上设置该值。  

## <a name="see-also"></a>另请参阅  
[常见问题](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[此版本驱动程序中的已知问题](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
