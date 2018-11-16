---
title: 发行说明-Microsoft ODBC Driver for Linux 和 macOS 上的 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 62270c3cce4b1a5f57874d6cd40c7c64ff409100
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600297"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Linux 和 macOS 上的 Microsoft ODBC Driver for SQL Server 的发行说明
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的新增功能

**支持的新分布**: Ubuntu 18.04

**添加功能**:

请参阅 Azure SQL 数据库和 SQL Server，有关详细信息的数据分类[数据分类](../data-classification.md)

支持 utf-8 服务器编码

SQLBrowseConnect

上的动态依赖关系`libcurl`:
- 此版本中，从开始`libcurl`程序包不是显式依赖关系。 `libcurl`包 OpenSSL 或 NSS 时需要使用 Azure 密钥保管库或 Azure Active Directory 身份验证。 如果您遇到的错误有关`libcurl`，确保已安装。

ConnectRetryCount 和 ConnectRetryInterval 连接字符串中的关键字与空闲连接复原能力 (有关详细信息，请参阅[Windows ODBC 驱动程序中的连接弹性](../windows/connection-resiliency-in-the-windows-odbc-driver.md)):
- 使用`SQL_COPT_SS_CONNECT_RETRY_COUNT`（只读） 来检索连接重试尝试次数。
- 使用`SQL_COPT_SS_CONNECT_RETRY_INTERVAL`（只读） 来检索连接重试间隔的时间长度。
- 默认情况下，将一次重新连接。


[Bug 修复](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的新增功能

**添加功能**:

为支持`SQL_COPT_SS_CEKCACHETTL`和`SQL_COPT_SS_TRUSTEDCMKPATHS`连接属性 (有关详细信息，请参阅[SQL Server 的 ODBC 驱动程序中使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` 允许控制的列加密密钥在本地缓存中存在的时间，以及刷新它
- `SQL_COPT_SS_TRUSTEDCMKPATHS` 允许应用程序限制为仅使用指定的列表的列主密匙的 AE 操作



对加载的支持`.rll`从默认位置 (有关详细信息，请参阅[安装文档中的资源文件正在加载部分](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[Bug 修复](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的新增功能

**支持的新分布**: macOS High Sierra 和 Ubuntu 17.10 

**性能改进**： 大于 10 倍时驱动程序转换到/从 UTF-8/16 的性能改进。

**添加功能**:

Always Encrypted 支持 BCP api

新的连接字符串属性 UseFMTOnly 导致驱动程序在特殊情况下要求临时表中使用旧的元数据。

对 Azure SQL 托管实例 （扩展个人预览版） 的支持。 
> [!NOTE]
> 使用托管实例时，有一些差异：
> -   不支持 FILESTREAM 
> -   本地文件系统访问不受支持，但是需要 tracefiles 之类的内容 
> -   从本地创建 UDT 不支持路径 
> -   不支持 Windows 集成身份验证 
> -   不支持 DTC 
> -   sa 帐户不存在 （默认帐户被称为 cloudSA）
> -   TDS 令牌错误 (0xAA) 返回不正确的服务器名称
> -   不支持数据库名称中的特殊字符 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] 不支持
> -   错误消息始终显示在英语中，而无论语言设置 （与 Azure 相同） 

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的新增功能  

ODBC Driver 13.1 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]添加了对始终加密和 Azure Active Directory 与 Microsoft SQL Server 2016 一起使用时支持。

**支持的新分布**： 在 macOS 上的 ODBC 驱动程序的第一个版本中支持 OS X 10.11 和 macOS 10.12。 Ubuntu 16.10 现在还支持，以及 Red Hat 6、 7 和 SUSE 12。 每个平台都有相关平台的包 （RPM 或 DEB） 轻松安装和配置。  请参阅[安装驱动程序](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)有关安装说明。

**unixODBC 驱动程序管理器 2.3.1 支持更改**: ODBC 驱动程序不再依赖于自定义包装的 unixODBC 驱动程序管理器 （RedHat 6 上除外），并改为依赖于分发包管理器来解决 UnixODBC 依赖关系从分发存储库。

**BCP API 支持**: Linux 和 macOS 的 ODBC 驱动程序现在支持使用[BCP API 函数 (**bcp_init**，等等。)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>新增的 Microsoft ODBC Driver 13.0 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Linux 上  
使用 SQL Server 的 Microsoft ODBC Driver 13.0，SQL Server 2014 和 SQL Server 2016 现在也支持。  

**支持的新分布**:

Ubuntu 以及 Red Hat 和 SUSE 现在受支持。 每个平台都有相关平台的包 （RPM 或 DEB） 轻松安装和配置。  请参阅[安装驱动程序](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)有关安装说明。

**unixODBC 驱动程序管理器 2.3.1 支持**： 除了较新的驱动程序管理器中，还有用于安装此依赖项，可方便地安装和配置包。  

**透明网络 IP 解析**： 透明网络 IP 解析是这种情况，第一个解析主机名的 IP 不在驱动程序的连接顺序会影响现有多子网故障转移功能的修订版本响应并且没有与主机名相关联的多个 Ip。

**TLS 1.2 支持**: Linux 上的 SQL Server 的 Microsoft ODBC Driver 13.0 现在支持 TLS 1.2 时用于保护与 SQL Server 的通信。

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>Linux 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的新增功能  
SUSE Linux 上的 ODBC 驱动程序（预览版）支持 64 位 SUSE Linux Enterprise 11 Service Pack 2。 有关详细信息，请参阅 [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md)。  

Linux 上的 ODBC 驱动程序支持 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]。 有关详细信息，请参阅[ODBC 驱动程序对高可用性和灾难恢复的 Linux 支持](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  

Linux 上的 ODBC 驱动程序支持与 Microsoft Azure SQL 数据库的连接。 有关详细信息，请参阅 [如何：使用 ODBC 连接到 Windows Azure SQL 数据库](https://msdn.microsoft.com/library/hh974312.aspx)。  

`-l`选项 （登录超时值） 添加到`bcp`。 有关详细信息，请参阅[使用 bcp 连接](../../../connect/odbc/linux-mac/connecting-with-bcp.md)。
