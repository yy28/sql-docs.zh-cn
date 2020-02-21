---
title: Windows 上的 Microsoft ODBC Driver for SQL Server 的功能 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: v-makouz
ms.author: genemi
ms.openlocfilehash: 6e3f7929c17b161d3534474d3d9ad99e559714d2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69653809"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver for SQL Server 的功能
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-174-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 17.4 for SQL Server

ODBC Driver 17.4 具有调整 TCP Keep-Alive 设置的功能。 可以通过将值添加到 Driver 或 DSN 注册表项来修改这些设置。 这些项位于系统数据源的 `HKEY_LOCAL_MACHINE\Software\ODBC\` 中，以及用户数据源的 `HKEY_CURRENT_USER\Software\ODBC\` 中。 对于 DSN，需要将这些值添加到 `...\Software\ODBC\ODBC.INI\<DSN Name>` 中，对于 Driver，则需要添加到 `...\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server` 中。

有关详细信息，请参阅 [ODBC 组件的注册表项](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。

值为 `REG_SZ`，如下所示：

- `KeepAlive` 控制 TCP 通过发送 keep-alive 数据包尝试验证空闲连接是否仍保持原样的频率。 默认为 30 秒。

- `KeepAliveInterval` 确定在收到响应之前分隔 keep-alive 重新传输的时间间隔。 默认值为 1 秒。



## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 13.1 for SQL Server

ODBC Driver 13.1 for SQL Server 不仅包含以前版本 (11) 的所有功能，还添加了在与 Microsoft SQL Server 2016 结合使用时，对 Always Encrypted 和 Azure Active Directory 身份验证的支持。  
  
始终加密允许客户端对客户端应用程序内的敏感数据进行加密，并且永远不向 SQL Server 显示加密密钥。 安装在客户端计算机上的启用始终加密的驱动程序通过在 SQL Server 客户端应用程序中对敏感数据进行加密和解密来实现此目标。 该驱动程序先对敏感列中的数据进行加密，然后再将该数据传递到 SQL Server，并且自动重写查询以便保留应用程序的语义。 同样，该驱动程序以透明方式对存储在加密数据库列（包含在查询结果中）中的数据进行解密。 有关详细信息，请参阅[在 ODBC 驱动程序中使用 Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)。
 
使用 Azure Active Directory，用户、DBA 和应用程序程序员可以将 Azure Active Directory 身份验证用作一种机制，通过这种机制可以使用 Azure Active Directory (Azure AD) 中的标识连接到 Microsoft Azure SQL 数据库和 Microsoft SQL Server 2016。 有关详细信息，请参阅[结合使用 Azure Active Directory 和 ODBC 驱动程序](../../../connect/odbc/using-azure-active-directory.md)和[使用 Azure Active Directory 身份验证连接到 SQL 数据库或 SQL 数据仓库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft ODBC Driver 11 for SQL Server（Windows 平台）  

适用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC 驱动程序包含 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中随附的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序的所有功能。 有关详细信息，请参阅 [SQL Server Native Client 编程](../../../relational-databases/native-client/sql-server-native-client-programming.md)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序基于 Windows 操作系统中随附的 ODBC 驱动程序。 有关详细信息，请参阅 [Windows 数据访问组件 SDK](https://msdn.microsoft.com/library/aa968814(VS.85).aspx)。  
  
该版本适用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC 驱动程序包含以下新功能：  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>用于指定登录超时的 bcp.exe -l 选项
 
-l 选项指定在尝试连接到服务器时 `bcp.exe` 登录 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的超时时间（以秒为单位）。 默认登录超时值为 15 秒。 登录超时必须是介于 0 和 65534 之间的数字。 如果提供的值不是数值或不在此范围内，则 `bcp.exe` 将生成错误消息。 值 0 指定无限超时。 登录超时时间小于（大约）10 秒不可靠。  
  
### <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持[识别驱动程序的连接池](https://msdn.microsoft.com/library/hh405031(VS.85).aspx)。 有关详细信息，请参阅 [ODBC Driver for SQL Server 中识别驱动程序的连接池](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。  
  
### <a name="asynchronous-execution-notification-method"></a>异步执行（通知方法）  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持[异步执行（通知方法）](https://msdn.microsoft.com/library/hh405038(VS.85).aspx)。 有关用法示例，请参阅[异步执行（通知方法）示例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)。  
  
### <a name="connection-resiliency"></a>连接复原
为了确保应用程序能与 Microsoft Azure SQL Database 保持连接，Windows 上的 ODBC 驱动程序可以还原空闲连接。 有关详细信息，请参阅 [Windows ODBC 驱动程序中的连接弹性](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)。  
  
## <a name="behavior-changes"></a>行为更改

在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中，如果显示宽度为 0，`sqlcmd.exe` 的 `-y0` 选项将导致输出在 1 MB 处被截断。
  
从 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 开始，当指定 `-y0` 时，对单列中可以检索的数据量没有任何限制。 `sqlcmd.exe` 现最多可流式传输 2GB（[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型最大值）列。  
  
另一个区别在于，现在，同时指定 `-h` 和 `-y0` 会生成一个错误报告，指出这些选项不兼容。 `-h` 用于指定要在列标题之间输出的行数且从未与 `-y0` 兼容，并已忽略（尽管未打印任何标题）。
  
`-y0` 可能导致服务器和网络上出现性能问题，具体取决于返回的数据大小。

## <a name="see-also"></a>另请参阅  
[Windows 上的 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
