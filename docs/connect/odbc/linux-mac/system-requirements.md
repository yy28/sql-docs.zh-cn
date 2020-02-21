---
title: 系统要求 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 49cb24120d6c476e5b03c4a0cad2ddda511a9360
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "76911186"
---
# <a name="system-requirements"></a>系统要求
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主题列出了使用 Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的要求。


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>Microsoft ODBC Driver 13、13.1 和 17 for SQL Server

Linux 和 macOS 驱动程序仅适用于以下操作系统的 64 位版本：

|操作系统|支持的驱动程序版本|
|------------------------------------|--------------------------------|
|Apple OS X 10.11 (El Capitan)|13、13.1、17.4|
|Apple macOS 10.12 (Sierra)|13、13.1、17.4|
|Apple macOS 10.13 (High Sierra)|17+| 
|Apple macOS 10.14 (Mojave)|17+| 
|Apple macOS 10.15 (Catalina)|17.5+| 
|Alpine Linux 3.11|17.5+| 
|Debian Linux 8|13、13.1、17.4| 
|Debian Linux 9|17+|
|Debian Linux 10|17.4+|
|Oracle Linux 8|17.5+|
|RedHat Enterprise Linux 6|13、13.1、17+|
|RedHat Enterprise Linux 7|13、13.1、17+|
|RedHat Enterprise Linux 8|17.4+|
|SuSE Linux Enterprise Server 11|13、13.1、17+ <br /><br /> **注意：** ODBC Driver 17 仅支持 SuSE Linux Enterprise Server 11 SP4|
|SuSE Linux Enterprise Server 12|13、13.1、17+|
|SuSE Linux Enterprise Server 15|17+|
|Ubuntu Linux 14.04|13、13.1、17.4|
|Ubuntu Linux 15.10|13、13.1|
|Ubuntu Linux 16.04|13、13.1、17+|
|Ubuntu Linux 16.10|13、13.1|
|Ubuntu Linux 17.04|17.4| 
|Ubuntu Linux 17.10|17.4|
|Ubuntu Linux 18.04|17+|
|Ubuntu Linux 18.10|17.4|
|Ubuntu Linux 19.04|17.3|
|Ubuntu Linux 19.10|17.5+| 

> [!NOTE]
> - 活动支持中的操作系统在驱动程序版本后显示“+”，没有加号的操作系统将显示给定操作系统支持的最后一个驱动程序版本

如[安装 ODBC Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)中所述，使用分发的程序包管理系统安装时，Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 13、13.1 和 17 版的安装包会自动解析驱动程序的依赖项。

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
-   针对 64 位 SQLLEN/SQLULEN 生成的 64 位 UnixODBC 2.3.0 驱动程序管理器。 Linux 上的 ODBC 驱动程序不支持更高版本的 64 位 UnixODBC 驱动程序管理器。 有关详细信息，请参阅 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 。  
  
-   用于 Red Hat Enterprise Linux 5（64 位）  的 ODBC 驱动程序需要以下程序包，并且可以在此处下载：[Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   用于 Red Hat Enterprise Linux 6（64 位）  的 ODBC 驱动程序需要以下程序包，并且可以在此处下载：[Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   用于 SUSE Linux Enterprise 11 Service Pack 2（64 位）  的 ODBC 驱动程序需要以下程序包，并且可以在此处下载：[Microsoft ODBC Driver 11 for SQL Server 预览版 - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>另请参阅
[安装驱动程序管理器](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[此版本驱动程序中的已知问题](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[发行说明](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
