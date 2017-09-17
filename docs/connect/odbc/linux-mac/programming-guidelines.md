---
title: "编程指南 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2e3aac41bd87f52998edf366d7c3da2326de3f26
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="programming-guidelines"></a>编程指南
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]编程功能[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 和为 13.1[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 macOS 和 Linux 上基于在 ODBC[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]本机客户端 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151))。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]本机客户端将基于 Windows 数据访问组件中的 ODBC ([ODBC 程序员参考](http://go.microsoft.com/fwlink/?LinkID=45250))。  

ODBC 应用程序可以使用多个活动结果集 (MARS) 和其他[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]特定功能包括`/usr/local/include/msodbcsql.h`后的 unixODBC 标头 (`sql.h`， `sqlext.h`， `sqltypes.h`，和`sqlucode.h`)。 然后，使用的相同符号名称[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-就像在 Windows ODBC 应用程序中的特定项。  

## <a name="available-features"></a>可用功能  
以下各节从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]适用于 ODBC 的本机客户端文档 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) 时在 macOS 和 Linux 上使用的 ODBC 驱动程序都有效：  

-   [与 SQL Server (ODBC) 通信](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [连接和查询的超时支持](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [游标](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [日期/时间改进 (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [执行查询 (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [处理错误和消息](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Kerberos 身份验证](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [大型 CLR 用户定义类型 (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [（除外分布式事务） 中执行事务 (ODBC)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [处理结果 (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [运行存储的过程](http://msdn.microsoft.com/library/ms131440.aspx)
-   [稀疏列支持 (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 加密](http://msdn.microsoft.com/library/ms131691.aspx)
-   [表值的参数](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [Utf-8 和 utf-16 命令和数据的 api](http://msdn.microsoft.com/library/ff878241.aspx)
-   [使用目录函数](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>不支持的功能

以下功能不验证在 macOS 和 Linux 上的 ODBC 驱动程序的此版本中正常工作：

-   故障转移群集连接
-   [透明网络 IP 解析](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution)
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

编码的客户端可以是以下项之一：
  -  UTF-8
  -  ISO 8859-1
  -  ISO 8859-2
  -  ISO 8859-3
  -  ISO 8859-4
  -  ISO 8859-5
  -  ISO 8859-6
  -  ISO 8859-7
  -  ISO 8859-8
  -  ISO 8859-9
  -  ISO 8859-13
  -  ISO 8859-15
  
SQLCHAR 数据必须是支持的字符集。 SQLWCHAR 数据必须是 UTF-16LE (Little Endian)。  

如果 SQLDescribeParameter 没有在服务器上指定 SQL 类型，驱动程序将使用在 SQLBindParameter 的 *ParameterType* 参数中指定的 SQL 类型。 如果在 SQLBindParameter 指定窄字符 SQL 类型，如 SQL_VARCHAR，驱动程序将转换所提供的数据从客户端代码页为默认值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]代码页。 (默认值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]代码页通常是 1252年。)如果不支持的客户端代码页，则它将设置为 utf-8。 在这种情况下，该驱动程序然后将 utf-8 数据转换为默认代码页。 但这样可能会发生数据丢失。 如果代码页 1252 无法表示某个字符，驱动程序会将该字符转换为一个问号 ('?')。 为避免此数据丢失，请在 SQLBindParameter 中指定一种 Unicode SQL 字符类型（例如 SQL_NVARCHAR）。 在这种情况下，该驱动程序将转换 utf-8 编码为 utf-16 而不会丢失数据中提供的 Unicode 数据。

没有 Windows 和 Linux 和 macOS 上的 iconv 库的多个版本之间的文本编码转换有所不同。 在代码页 1255 （希伯来语） 中编码的文本数据具有一个码位 (0xCA)，在转换时的行为方式不同。 将此字符转换为 Unicode Windows 上生成 0x05BA 一个 utf-16 码的位。 将转换为 Unicode 在 macOS 和 Linux 上使用 libiconv 版本早于 1.15 产生的 0x00CA 的一个 utf-16 码位。

当在 SQLPutData 缓冲区上拆分 UTF-8 多字节字符或 UTF-16 代理项时，这会导致数据损坏。 使用用于流式传输不会在部分字符编码中结束的 SQLPutData 的缓冲区。  

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

