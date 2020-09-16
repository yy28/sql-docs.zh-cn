---
title: Linux 和 macOS 上的 ODBC 驱动程序的已知问题
description: 了解 Linux 和 macOS 上有关 Microsoft ODBC Driver for SQL Server 的已知问题，以及解决连接问题的步骤。
ms.date: 09/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1057252f896b62a5659b53aa53eb2f5c6d9b17ea
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288019"
---
# <a name="known-issues-for-the-odbc-driver-on-linux-and-macos"></a>Linux 和 macOS 上的 ODBC 驱动程序的已知问题

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文包含 Linux 和 macOS 上的 Microsoft ODBC Driver for SQL Server 13、13.1 和 17 的已知问题列表。 它还包含用于排查连接问题的步骤。

## <a name="known-issues"></a>已知问题

其他问题将在 [SQL Server 驱动程序博客](https://techcommunity.microsoft.com/t5/SQL-Server/bg-p/SQLServer/label-name/SQLServerDrivers)上发布。  

- 由于系统库限制，Alpine Linux 支持较少的字符编码和区域设置。 例如 en_US.UTF-8 不可用。 有关详细信息，请参阅 [musl libc 与 glibc 功能之间的差异](https://wiki.musl-libc.org/functional-differences-from-glibc.html)。

- Windows、Linux 和 macOS 可以采用不同方式转换来自专用区 (PUA) 或最终用户定义的字符 (EUDC) 的字符。 在服务器上执行的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 内的转换将使用 Windows 转换库。 驱动程序中的转换使用 Windows、Linux 或 macOS 转换库。 在执行这些转换时，每个库可能会产生不同的结果。 有关详细信息，请参阅[最终用户定义的字符和专用区字符](/windows/desktop/Intl/end-user-defined-characters)。

- 如果客户端采用 UTF-8 编码，驱动程序管理器不会始终将 UTF-8 正确转换为 UTF-16。 目前，当字符串中的一个或多个字符不是有效的 UTF-8 字符时，会发生数据损坏。 ASCII 字符已正确映射。 当调用 SQLCHAR 版本的 ODBC API（例如 SQLDriverConnectA）时，驱动程序管理器尝试此转换。 当调用 SQLWCHAR 版本的 ODBC API（例如，SQLDriverConnectW）时，驱动程序管理器不会尝试此转换。  

- SQLBindParameter 的 ColumnSize 参数指的是 SQL 类型的字符数，而 BufferLength 是应用程序缓冲区中的字节数    。 但是，如果 SQL 数据类型为 `varchar(n)` 或 `char(n)` 且应用程序将参数绑定为 SQL_C_CHAR 或 SQL_C_VARCHAR 并且客户端的字符编码为 UTF-8，可能会从驱动程序收到“字符串数据，右截断”错误，即使 ColumnSize 的值与服务器上的数据类型大小保持一致  。 出现此错误是因为字符编码之间的转换可能会更改数据的长度。 例如，右单引号字符 (U+2019) 以 CP-1252 编码为单字节 0x92，但以 UTF-8 则编码为 3 个字节序列 - 0xe2 0x80 0x99。

例如，如果采用 UTF-8 编码，并且为 out 参数的 SQLBindParameter 中的 BufferLength 和 ColumnSize 均指定 1，然后尝试检索存储在服务器上的 `char(1)` 列中的前一个字符（使用 CP-1252），则驱动程序会尝试将其转换为 3 个字节的 UTF-8 编码，但无法使结果适合 1 个字节的缓冲区    。 如果条件相反，它会比较 SQLBindParameter 中的 ColumnSize 和 BufferLength，然后在客户端和服务器上的不同代码页之间进行转换    。 因为 *ColumnSize* 的值 1 小于 *BufferLength* 的值（例如）3，因此驱动程序将生成一个错误。 要避免此错误，请确保转换后的数据长度适合指定的缓冲区或列。 请注意，对于 `varchar(n)` 类型，ColumnSize 不能大于 8000  。

## <a name="troubleshooting-connection-problems"></a><a id="connectivity"></a> 排查连接问题  

如果使用 ODBC 驱动程序无法连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，请使用以下信息确定问题原因。  
  
最常见的连接问题是安装两个 UnixODBC 驱动程序管理器的副本。 搜索 /usr 以查找 libodbc\*.so\*。 如果看到多个版本的文件，则（可能）安装了多个驱动程序管理器。 你的应用程序可能会使用错误的版本。
  
通过编辑 `/etc/odbcinst.ini` 文件以包含具有这些条目的如下部分来启用连接日志：

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
如果连接再次失败并且未看到日志文件，则计算机上（可能）存在两个驱动程序管理器的副本。 否则，日志输出应该类似于以下内容：  
  
```
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 17 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
如果 ASCII 字符编码不是 UTF-8，例如： 
  
```
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
安装了多个驱动程序管理器并且应用程序使用的是错误的管理器，或者驱动程序管理器未正确构建。  
  
有关解决这种连接失败的详细信息，请参阅：  

- [解决 SQL 连接问题的步骤](https://docs.microsoft.com/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
- [SQL Server 2005 连接问题疑难解答 - 第 I 部分](https://techcommunity.microsoft.com/t5/sql-server/sql-server-2005-connectivity-issue-troubleshoot-part-i/ba-p/383034)  
  
- [带有连接环形缓冲区的 SQL Server 2008 中的连接疑难解答](https://techcommunity.microsoft.com/t5/sql-server/connectivity-troubleshooting-in-sql-server-2008-with-the/ba-p/383393)  
  
- [SQL Server 身份验证疑难解答](/archive/blogs/sqlsecurity/sql-server-authentication-troubleshooter)  

## <a name="next-steps"></a>后续步骤

有关 ODBC 驱动程序安装说明，请参阅以下文章：

- [安装 Linux 上的 Microsoft ODBC Driver for SQL Server](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [安装 macOS 上的 Microsoft ODBC Driver for SQL Server](install-microsoft-odbc-driver-sql-server-macos.md)

有关详细信息，请参阅[编程准则](programming-guidelines.md)和[发行说明](release-notes-odbc-sql-server-linux-mac.md)。  
