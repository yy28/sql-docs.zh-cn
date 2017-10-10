---
title: "发行说明-Microsoft ODBC Driver for SQL Server 在 Linux 和 macOS 上 |Microsoft 文档"
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
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 84bb78e184f1bca9e683aeebf46b178e3a7dd61f
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>在 Linux 和 macOS 上的 SQL Server 的 Microsoft ODBC 驱动程序的发行说明
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

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

