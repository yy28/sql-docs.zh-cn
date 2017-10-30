---
title: "Installing the Driver Manager |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
caps.latest.revision: 59
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ca46eb4fbb6203191a7aace3946daad8361b224
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="installing-the-driver-manager"></a>安装驱动程序管理器
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主题包含若要使用 Microsoft ODBC Driver 11、 13 或 13.1 for SQL Server 在 Linux 和 macOS 上安装 unixODBC 驱动程序管理器使用的说明。  

> [!IMPORTANT]  
> 在安装 unixODBC 驱动程序管理器之前，删除安装在计算机上的任何驱动程序管理器包。 安装 unixODBC 驱动程序管理器可能会导致现有驱动程序管理器出现故障。  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-130-and-131"></a>安装 Microsoft ODBC 驱动程序为 13.0 和 13.1 驱动程序管理器
包管理系统的自动得到解决你安装 Microsoft ODBC 驱动程序为 13.0 或 13.1 for SQL Server 上 Linux 或 macOS 按照中的说明驱动程序管理器依赖关系[安装 Microsoft ODBC 驱动程序有关在 Linux 或 macOS 上的 SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>为 Microsoft ODBC Driver 11 for SQL Server 安装驱动程序管理器  

（SUSE 和仅限 Red Hat Linux。）

**使用安装脚本**  
  
> [!IMPORTANT]  
> 这些说明是指`msodbcsql-11.0.2270.0.tar.gz`，即 Red Hat Linux 的安装文件。 如果你要安装适用于 SUSE Linux 预览，文件名是`msodbcsql-11.0.2260.0.tar.gz`。  

若要安装驱动程序管理器：  
  
1.  请确保具有根权限。  
  
2.  转到目录其中[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ODBC 驱动程序下载放置的文件称为`msodbcsql-11.0.2270.0.tar.gz`。 确保所拥有的 \*.tar.gz 文件与你的 Linux 版本匹配。 若要提取的文件，请执行以下命令： **tar xvzf msodbcsql 11.0.2270.0.tar.gz**。  

3.  将更改为`msodbcsql-11.0.2270.0`目录，你应该看到名为的文件的存在`build_dm.sh`。 你可以运行`build_dm.sh`安装 unixODBC 驱动程序管理器。

4.  若要查看可用选项的列表，请执行以下命令： **./build_dm.sh-帮助**。  
  
5.  当你准备好安装，并且如果你的计算机可以访问外部站点通过 FTP，执行以下命令： **./build_dm.sh**。

如果你的计算机无法访问外部站点通过 FTP，获取`unixODBC-2.3.0.tar.gz`。 你可以获取`unixODBC-2.3.0.tar.gz`从[http://www.unixodbc.org](http://www.unixodbc.org/)。单击**下载**页后，可以转到下载页面左侧的链接。 然后，单击相应链接以下载 unixODBC-2.3.0（而非 unixODBC-2.3.1）。 此版本的不支持 unixODBC 2.3.1 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 执行以下命令以开始 unixODBC 驱动程序管理器安装： **./build_dm.sh-下载 url = file://unixODBC-2.3.0.tar.gz**。  

6.  类型**是**继续进行解压缩文件。 完成这部分过程最多需要 5 分钟。  

7.  该脚本停止运行后，按照屏幕上的说明来安装 unixODBC 驱动程序管理器。

现在可以随时安装该驱动程序。 请参阅[安装 Microsoft ODBC Driver for SQL Server 在 Linux 和 macOS 上](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)有关详细信息。  

**手动安装**

如果无法完成安装脚本，请自行配置并生成合适的驱动程序管理器。

1.  删除所有已安装的旧版 unixODBC（例如 unixODBC 2.2.11）。 在 Red Hat Enterprise Linux 5 或 6 上，执行以下命令： **yum 删除 unixODBC**。 SUSE Linux Enterprise 上**zypper 删除 unixODBC**。  
  
2.  转到[http://www.unixodbc.org](http://www.unixodbc.org/)。单击**下载**页后，可以转到下载页面左侧的链接。 然后，单击相应链接以将文件 unixODBC-2.3.0.tar.gz 保存到计算机。 此版本的不支持 UnixODBC 2.3.1 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
3.  在你的 Linux 计算机上执行该命令： **tar xvzf unixODBC 2.3.0.tar.gz**。  
  
4.  转到 unixODBC-2.3.0 目录。  
  
5.  在命令提示符下执行命令： **CPPFLAGS ="-DSIZEOF_LONG_INT = 8"**。  
  
6.  在命令提示符下执行命令：**导出 CPPFLAGS**。  
  
7.  在命令提示符下执行命令： **"。 / 配置-前缀 = / usr-libdir = / usr/lib64-sysconfdir = / 等-启用 gui = 否 — 启用驱动程序 = 否 — 启用 iconv-与-iconv-char-enc = UTF8-与-iconv-ucode-enc = UTF16LE"**.  
  
8.  在命令提示符，（root 登录），执行该命令：**使**。  
  
9. 在命令提示符，（root 登录），执行该命令：**使安装**。  

现在可以随时安装该驱动程序。 请参阅[安装 Microsoft ODBC Driver for SQL Server 在 Linux 和 macOS 上](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)有关详细信息。  
  
## <a name="see-also"></a>另请参阅
[安装 Microsoft ODBC Driver for SQL Server 在 Linux 和 macOS 上](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[此版本驱动程序中的已知问题](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes.md)

