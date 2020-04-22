---
title: 安装驱动程序管理器
description: 本文介绍了如何安装 unixODBC 驱动程序管理器，以用于 Linux 和 macOS 上所有版本的 Microsoft ODBC Driver for SQL Server。
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba758f3c95ef3285424cafe676df46e5d3df7b34
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528241"
---
# <a name="installing-the-driver-manager"></a>安装驱动程序管理器
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文包含说明 Linux 和 macOS 上的 SQL Server 与所有版本的 Microsoft ODBC 驱动程序安装 unixODBC 驱动程序管理器使用。  

> [!IMPORTANT]  
> 在安装 unixODBC 驱动程序管理器之前，删除安装在计算机上的任何驱动程序管理器包。 安装 unixODBC 驱动程序管理器可能会导致现有驱动程序管理器出现故障。  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>为 Microsoft ODBC Driver 13、13.1 和 17 安装驱动程序管理器
如果按照以下文章中的说明操作，在 Linux 或 macOS 上为 SQL Server 安装 Microsoft ODBC 驱动程序 13、13.1 或 17 时，包管理系统会自动解析驱动程序管理器依赖性：

- [安装 Linux 上的 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [安装 macOS 上的 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>为 Microsoft ODBC Driver 11 for SQL Server 安装驱动程序管理器  

（SUSE 和仅限 Red Hat Linux。）

**使用安装脚本**  
  
> [!IMPORTANT]  
> 这些说明参考 Red Hat Linux 的安装文件 `msodbcsql-11.0.2270.0.tar.gz`。 如果要安装适用于 SUSE Linux 的预览版，则文件名为 `msodbcsql-11.0.2260.0.tar.gz`。  

若要安装驱动程序管理器：  
  
1.  请确保具有根权限。  
  
2.  转到 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC 驱动程序下载放置名为 `msodbcsql-11.0.2270.0.tar.gz` 的文件的目录。 确保所拥有的 \*.tar.gz 文件与你的 Linux 版本匹配。 若要提取文件，请执行以下命令：**tar xvzf msodbcsql-11.0.2270.0.tar.gz**。  

3.  转到 `msodbcsql-11.0.2270.0` 目录，你应在此处看到一个名为 `build_dm.sh` 的文件。 你可以运行`build_dm.sh`来安装 unixODBC 驱动程序管理器。

4.  若要查看可用选项列表，请执行以下命令： **./build_dm.sh --help**。  
  
5.  当已准备好安装且计算机可以通过 FTP 访问外部站点时，执行以下命令： **./build_dm.sh**。

如果计算机无法通过 FTP 访问外部站点，请获取 `unixODBC-2.3.0.tar.gz`。 可以从 [http://www.unixodbc.org](http://www.unixodbc.org/) 获取 `unixODBC-2.3.0.tar.gz` 。单击页面左侧的“下载”链接，转到下载页面  。 然后，单击相应链接以下载 unixODBC-2.3.0（而非 unixODBC-2.3.1）。 该版本的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不支持 unixODBC-2.3.1。 执行以下命令以开始 unixODBC 驱动程序管理器安装： **./build_dm.sh --download-url=file://unixODBC-2.3.0.tar.gz**。  

6.  键入 YES 以继续解压缩文件  。 完成这部分过程最多需要 5 分钟。  

7.  该脚本停止运行后，按照屏幕上的说明来安装 unixODBC 驱动程序管理器。

现在可以随时安装该驱动程序。 有关详细信息，请参阅 [Linux ](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) 或 [macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md) 的 ODBC 驱动程序安装说明。

**手动安装**

如果无法完成安装脚本，请自行配置并生成合适的驱动程序管理器。

1.  删除所有已安装的旧版 unixODBC（例如 unixODBC 2.2.11）。 在 Red Hat Enterprise Linux 5 或 6 上，执行以下命令：**yum remove unixODBC**。 SUSE Linux enterprise **zypper 删除 unixODBC**。  
  
2.  转到[http://www.unixodbc.org](http://www.unixodbc.org/)。单击页面左侧的“下载”链接，转到下载页面  。 然后，单击相应链接以将文件 unixODBC-2.3.0.tar.gz 保存到计算机。 该版本的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不支持 UnixODBC-2.3.1。  
  
3.  在你的 Linux 计算机上执行该命令： **tar xvzf unixODBC-2.3.0.tar.gz**。  
  
4.  转到 unixODBC-2.3.0 目录。  
  
5.  在命令提示符下，执行以下命令：**CPPFLAGS="-DSIZEOF_LONG_INT=8"** 。  
  
6.  在命令提示符处，执行以下命令：**export CPPFLAGS**。  
  
7.  在命令提示符处，执行以下命令： **"./configure --prefix=/usr --libdir=/usr/lib64 --sysconfdir=/etc --enable-gui=no --enable-drivers=no --enable-iconv --with-iconv-char-enc=UTF8 --with-iconv-ucode-enc=UTF16LE"** .  
  
8.  在命令提示符下（作为根登录），执行以下命令：**make**。  
  
9. 在命令提示符下（作为根登录），执行以下命令：**make install**。  

现在可以随时安装该驱动程序。 有关详细信息，请参阅 [Linux ](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) 或 [macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md) 的 ODBC 驱动程序安装说明。
  
## <a name="see-also"></a>另请参阅

- [安装 Linux 上的 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [安装 macOS 上的 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)
- [发行说明](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
