---
title: 系统要求 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2459a9f57f3591db1107994d0b18770690f22724
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921179"
---
# <a name="system-requirements"></a>系统要求

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主题列出了使用 Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的要求。

## <a name="sql-version-compatibility"></a>SQL 版本兼容性

Linux 和 macOS 驱动程序 SQL 版本兼容性与 [Windows 驱动程序 SQL 版本兼容性](../windows/system-requirements-installation-and-driver-files.md#sql-version-compatibility)相同。

## <a name="operating-system-support"></a>操作系统支持

以下操作系统的 64 位版本支持 Linux 和 macOS 驱动程序的版本 17、13.1 和 13：

|支持的操作系统     |17.5|17.4|17.3|17.2|17.1|17.0|13.1|13|
|-------------------------------|----|----|----|----|----|----|----|--|
|Apple OS X 10.11 (El Capitan)  | |Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.12 (Sierra)     | |Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.13 (High Sierra)|Y|Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.14 (Mojave)     |Y|Y|Y| | | | | |
|Apple macOS 10.15 (Catalina)   |Y| | | | | | | |
|Alpine Linux 3.11              |Y| | | | | | | |
|Debian Linux 8                 | |Y|Y|Y|Y|Y|Y|Y|
|Debian Linux 9                 |Y|Y|Y|Y|Y|Y|Y|Y|
|Debian Linux 10                |Y|Y| | | | | | |
|Oracle Linux 8                 |Y| | | | | | | |
|RedHat Enterprise Linux 6      |Y|Y|Y|Y|Y|Y|Y|Y|
|RedHat Enterprise Linux 7      |Y|Y|Y|Y|Y|Y|Y|Y|
|RedHat Enterprise Linux 8      |Y|Y| | | | | | |
|SUSE Linux Enterprise Server 11<sup>1</sup>|Y|Y|Y|Y|Y|Y|Y|Y|
|SUSE Linux Enterprise Server 12|Y|Y|Y|Y|Y|Y|Y|Y|
|SUSE Linux Enterprise Server 15|Y|Y|Y| | | | | |
|Ubuntu Linux 14.04             | |Y|Y|Y|Y|Y|Y|Y|
|Ubuntu Linux 16.04             |Y|Y|Y|Y|Y|Y|Y|Y|
|Ubuntu Linux 18.04             |Y|Y|Y|Y| | | | |
|Ubuntu Linux 19.10             |Y| | | | | | | |

<sup>1</sup> ODBC Driver 17 仅支持 SUSE Linux Enterprise Server 11 SP4

如[安装 ODBC Driver (Linux)](installing-the-microsoft-odbc-driver-for-sql-server.md) 和[安装 ODBC Driver (macOS) ](install-microsoft-odbc-driver-sql-server-macos.md)中所述，使用分发的程序包管理系统安装时，Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 13、13.1 和 17 版的安装包会自动解析驱动程序的依赖项。

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
* 针对 64 位 SQLLEN/SQLULEN 生成的 64 位 UnixODBC 2.3.0 驱动程序管理器。 Linux 上的 ODBC 驱动程序不支持更高版本的 64 位 UnixODBC 驱动程序管理器。 有关详细信息，请参阅 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 。  
  
* 用于 Red Hat Enterprise Linux 5（64 位）  的 ODBC 驱动程序需要以下程序包，并且可以在此处下载：[Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `e2fsprogs-libs`  
  * `krb5-libs`  
  * `openssl`  
  
* 用于 Red Hat Enterprise Linux 6（64 位）  的 ODBC 驱动程序需要以下程序包，并且可以在此处下载：[Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `libuuid`  
  * `krb5-libs`  
  * `openssl`  
  
* 用于 SUSE Linux Enterprise 11 Service Pack 2（64 位）  的 ODBC 驱动程序需要以下程序包，并且可以在此处下载：[Microsoft ODBC Driver 11 for SQL Server 预览版 - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
  * `glibc`  
  * `libstdc++46`  
  * `libgcc46`  
  * `libuuid1`  
  * `krb5`  
  * `libopenssl0_9_8`  
  
## <a name="see-also"></a>另请参阅

[安装驱动程序管理器](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)  
[此版本驱动程序中的已知问题](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  
[发行说明](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
