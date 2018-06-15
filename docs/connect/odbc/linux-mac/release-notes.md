---
title: 发行说明-Microsoft ODBC Driver for SQL Server 在 Linux 和 macOS 上 |Microsoft 文档
ms.custom: ''
ms.date: 04/04/2018
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
ms.openlocfilehash: bddb826772d1c6ad7e33dce92b1e2615779b8931
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853292"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>在 Linux 和 macOS 上的 SQL Server 的 Microsoft ODBC 驱动程序的发行说明
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新增内容[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上

**添加功能**:

支持`SQL_COPT_SS_CEKCACHETTL`和`SQL_COPT_SS_TRUSTEDCMKPATHS`连接属性 (有关详细信息，请参阅[Using Always Encrypted with ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` 允许控制本地缓存的列加密密钥存在的时间，以及刷新它
- `SQL_COPT_SS_TRUSTEDCMKPATHS` 允许应用程序限制为仅使用指定的列表的列主密钥的自动曝光操作



对加载支持`.rll`从默认位置 (有关详细信息，请参阅[安装文档中的资源文件加载部分](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[Bug 修复](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>中[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC 驱动程序 17[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 和 macOS 上

**支持的新分发**: macOS 高 Sierra 和 Ubuntu 17.10 

**性能改进**： 大于 10 倍时驱动程序将转换为 / 从 UTF 8/16 的性能改进。

**添加功能**:

BCP api 始终加密支持

新的连接字符串属性 UseFMTOnly 会导致在特殊情况下需要临时表使用旧的元数据的驱动程序。

Azure SQL 托管实例 （扩展特邀预览阶段） 的支持。 
> [!NOTE]
> 在使用托管实例时，有一些差异：
> -   不支持 FILESTREAM 
> -   本地文件系统访问是不受支持，但需要 tracefiles 之类的内容 
> -   从本地创建 UDT 不支持路径 
> -   不支持 Windows 集成身份验证 
> -   不支持 DTC 
> -   'sa' 帐户不存在 （默认帐户称为 cloudSA）
> -   TDS 令牌错误 (0xAA) 返回不正确的服务器名称
> -   不支持数据库名称中的特殊字符 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] 不支持
> -   错误消息将始终显示在英语，而不考虑语言设置 （与 Azure 相同） 

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>中[!INCLUDE[msCoName](../../../includes/msconame_md.md)]的 ODBC Driver 13.1[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 和 macOS 上  

有关 ODBC Driver 13.1[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]增加了始终加密和 Azure Active Directory 与 Microsoft SQL Server 2016 结合使用时。

**支持的新分发**: OS X 10.11 和 macOS 10.12 支持在 macOS 上 ODBC 驱动程序的第一个版本中。 Ubuntu 16.10 现在还支持，以及 Red Hat 6，7 和 SUSE 12。 每个平台都有平台相关的包 （RPM 或 DEB） 以减轻安装和配置。  请参阅[驱动程序的安装](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)有关安装说明。

**unixODBC 驱动程序管理器 2.3.1 支持更改**: ODBC 驱动程序不再依赖于自定义包装的 unixODBC 驱动程序管理器 （在 RedHat 6 上除外），并改为依赖于分发包管理器来解析 UnixODBC 依赖项从分发的存储库。

**BCP API 支持**： 的 Linux 和 macOS ODBC 驱动程序现在支持使用[BCP API 函数 (**bcp_init**等。)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>什么是新的 Microsoft ODBC 驱动程序中为 13.0[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 上  
使用 SQL Server 的 Microsoft ODBC 驱动程序 13.0，SQL Server 2014 和 SQL Server 2016 现在还支持。  

**支持的新分发**:

Ubuntu 以及 Red Hat 和 SUSE 现在受支持。 每个平台都有平台相关的包 （RPM 或 DEB） 以减轻安装和配置。  请参阅[驱动程序的安装](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)有关安装说明。

**unixODBC 驱动程序管理器 2.3.1 支持**： 除了较新的驱动程序管理器中，还有安装实现轻松安装和配置此依赖关系的包。  

**透明网络 IP 解析**： 透明网络 IP 解析为现有影响，第一个解析主机名的 IP 不这种情况中的驱动程序的连接顺序的多子网故障转移功能的修订版本响应并且没有与主机名相关联的多个 Ip。

**TLS 1.2 支持**: Linux 上的 SQL Server 的 Microsoft ODBC 驱动程序 13.0 现在支持 TLS 1.2，当使用与 SQL Server 的安全通信。

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>新增内容[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 11 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 上  
SUSE Linux 上的 ODBC 驱动程序（预览版）支持 64 位 SUSE Linux Enterprise 11 Service Pack 2。 有关详细信息，请参阅[系统要求](../../../connect/odbc/linux-mac/system-requirements.md)。  

在 Linux 上的 ODBC 驱动程序支持[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]。 有关详细信息，请参阅[上针对高可用性、 灾难恢复的 Linux 支持 ODBC 驱动程序](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  

Linux 上的 ODBC 驱动程序支持与 Microsoft Azure SQL 数据库的连接。 有关详细信息，请参阅 [如何：使用 ODBC 连接到 Windows Azure SQL 数据库](http://msdn.microsoft.com/library/hh974312.aspx)。  

`-l`选项 （登录超时值） 已添加到`bcp`。 有关详细信息，请参阅[使用连接**bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)。
