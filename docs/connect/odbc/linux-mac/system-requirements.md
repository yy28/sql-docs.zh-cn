---
title: "系统要求 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 75c8c9daea3f26dc694ae66597649f399a986456
ms.contentlocale: zh-cn
ms.lasthandoff: 09/22/2017

---
# <a name="system-requirements"></a>系统要求
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主题列出使用的要求[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 和 macOS 上。

## <a name="microsoft-odbc-driver-13-and-131-for-sql-server"></a>Microsoft ODBC Driver 13 和 13.1 for SQL Server

Linux 和 macOS 驱动程序是仅适用于以下操作系统的 64 位版本：

- Apple macOS 10.12 (Sierra)
- Apple OS X 10.11 (El Capitan)
- Debian Linux 8
- RedHat Enterprise Linux 6
- RedHat Enterprise Linux 7
- SuSE Linux Enterprise Server 11
- SuSE Linux Enterprise Server 12
- Ubuntu Linux 14.04
- Ubuntu Linux 15.10
- Ubuntu Linux 16.04
- Ubuntu Linux 16.10

安装打包以[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 和为 13.1[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 和 macOS 上解决驱动程序的依赖关系中所述使用您的分发的包管理系统的安装时自动[驱动程序的安装](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
-   针对 64 位 SQLLEN/SQLULEN 生成的 64 位 UnixODBC 2.3.0 驱动程序管理器。 Linux 上的 ODBC 驱动程序不支持更高版本的 64 位 UnixODBC 驱动程序管理器。 有关详细信息，请参阅 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 。  
  
-   ODBC 驱动程序**Red Hat Enterprise Linux 5 （64 位）**需要以下包，并且可以在此处下载： [Microsoft ODBC Driver 11 for SQL Server-Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   glibc  
    -   libgcc  
    -   libstdc++  
    -   e2fsprogs-libs  
    -   krb5-libs  
    -   openssl  
  
-   ODBC 驱动程序**Red Hat Enterprise Linux 6 （64 位）**需要以下包，并且可以在此处下载： [Microsoft ODBC Driver 11 for SQL Server-Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   glibc  
    -   libgcc  
    -   libstdc++  
    -   libuuid  
    -   krb5-libs  
    -   openssl  
  
-   ODBC 驱动程序**SUSE Linux Enterprise 11 Service Pack 2 （64 位）**需要以下包，并且可以在此处下载： [for SQL Server-SUSE Linux 的 Microsoft ODBC Driver 11 预览](http://go.microsoft.com/fwlink/?LinkId=264916)  
    -   glibc  
    -   libstdc++46  
    -   libgcc46  
    -   libuuid1  
    -   krb5  
    -   libopenssl0_9_8  
  
## <a name="see-also"></a>另请参阅
[安装驱动程序管理器](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[此版本驱动程序中的已知问题](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[发行说明](../../../connect/odbc/linux-mac/release-notes.md)  

