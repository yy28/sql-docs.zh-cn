---
title: "安装 SQL Server 2016 的硬件和软件要求 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/23/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
caps.latest.revision: 333
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 952d6202918895d0d6f7b6496bff1185ccc4170b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>安装 SQL Server 的硬件和软件要求

本主题列出了在 Windows 操作系统上安装和运行 [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] 至少需要满足的硬件和软件要求。 

[!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)] 现已开始支持 Linux 上的 [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)]。 有关信息，请参阅 [Linux 上 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion_md.md)] 的硬件和软件要求](../../linux/sql-server-linux-setup.md#system)。 

> 本主题适用于 [!INCLUDE[ss2016](../../includes/sssql15-md.md)] 及更高版本。 有关与以前版本的 SQL Server 相关的内容，请参阅[安装 SQL Server 2014 的硬件和软件要求](https://msdn.microsoft.com/library/ms143506(v=sql.120).aspx)。 
  
**进行试用：**  
  
-   从 [**评估中心**下载 SQL Server。](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) 
  
-    加速已安装有 [**SQL Server 2016**](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) 的虚拟机。  
  
 **以下注意事项适用于所有版本：**  
  
-   我们建议在使用 NTFS 或 ReFS 文件格式的计算机上运行 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 。 支持但建议不要在使用 FAT32 文件系统的计算机上安装 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] ，因为它没有 NTFS 或 ReFS 文件系统安全。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将阻止在只读驱动器、映射的驱动器或压缩驱动器上进行安装。  
  
-   如果通过远程桌面连接 RDC 客户端上本地资源中的介质来启动安装程序，安装将会失败。 若要执行远程安装，介质必须处于网络共享状态，或是物理计算机或虚拟机的本地介质。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装介质要么处于网络共享状态，要么是映射的驱动器、本地驱动器，或者是虚拟机的 ISO。  
  
-   安装 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 时，必须先安装 .NET 4.6.1 必备组件。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 处于选中状态时，安装程序将自动安装 .NET 4.6.1。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序安装该产品所需的以下软件组件：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序支持文件  
  
-   有关在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 上安装 [!INCLUDE[win8](../../includes/win8-md.md)]的最低版本要求，请参阅 [在 Windows Server 2012 或 Windows 8 上安装 SQL Server](http://support.microsoft.com/kb/2681562) (http://support.microsoft.com/kb/2681562)。  
  
##  <a name="hwswr"></a> 硬件和软件要求  
以下要求适用于所有安装：  
  
|组件|要求|  
|---------------|-----------------|  
|.NET Framework|[!INCLUDE[sql2016](../../includes/sssql15-md.md)] RC1 和更高版本需要 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 才能运行数据库引擎、Master Data Services 或复制。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 安装程序会自动安装 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。 还可以从 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 适用于 Windows 的 Microsoft .NET Framework 4.6（Web 安装程序） [中手动安装](http://support.microsoft.com/kb/3045560)。<br/><br/> 有关 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 的详细信息、建议和指南，请参阅 [面向开发人员的 .NET Framework 部署指南](http://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx)。<br/><br/>在安装[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]4.6 之前， [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)] 和 [需要](http://support.microsoft.com/kb/2919355) KB2919355 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。|  
|网络软件|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 支持的操作系统具有内置网络软件。 独立安装的命名实例和默认实例支持以下网络协议：共享内存、命名管道、TCP/IP 和 VIA。<br/><br/> 注意：故障转移群集不支持共享内存和 VIA。<br/><br/> 还要注意，不推荐使用 VIA 协议。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> <br/><br/> 有关网络协议和网络库的详细信息，请参阅 [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md)。|  
|硬盘|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 要求最少 6 GB 的可用硬盘空间。<br/><br/> 磁盘空间要求将随所安装的 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 组件不同而发生变化。 有关详细信息，请参阅本主题靠后部分中的 [硬盘空间要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) 。 有关支持的数据文件存储类型的信息，请参阅 [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)。|  
|驱动器|从磁盘进行安装时需要相应的 DVD 驱动器。|  
|监视器|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 要求有 Super-VGA (800x600) 或更高分辨率的显示器。|  
|Internet|使用 Internet 功能需要连接 Internet（可能需要付费）。|  
  
 注意：在虚拟机上运行 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的速度要慢于在本机运行，因为虚拟化会产生系统开销。  
  
 对于 PolyBase 功能没有附加的硬件和软件要求。 有关详细信息，请参阅 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
##  <a name="pmosr"></a> 处理器、内存和操作系统要求  
 以下内存和处理器要求适用于所有版本的 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]：  
  
|组件|要求|  
|---------------|-----------------|  
|内存*|**最低要求：**<br/><br/> Express 版本：512 MB<br/><br/> 所有其他版本：1 GB<br/><br/> **建议：**<br/><br/> Express 版本：1 GB<br/><br/> 所有其他版本：至少 4 GB 并且应该随着数据库大小的增加而增加，以便确保最佳的性能。|  
|处理器速度|**最低要求：** x64 处理器：1.4 GHz<br/><br/> **建议** ：2.0 GHz 或更快|  
|处理器类型|x64 处理器：AMD Opteron、AMD Athlon 64、支持 Intel EM64T 的 Intel Xeon、支持 EM64T 的 Intel Pentium IV|  
  
> [!NOTE]  
>  仅 x64 处理器支持 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的安装。 x86 处理器不再支持此安装。  
  
 \*内存至少必须有 2GB RAM，才能在 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 中安装 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 组件。此要求不同于 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的最低内存要求。 有关安装 DQS 的信息，请参阅 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
 **WOW64 支持：**  
  
 WOW64（Windows 64 位上的 Windows 32 位）是 Windows 64 位版本中的一项功能，使用该功能可以在 32 位模式下本机运行 32 位应用程序。 尽管基础操作系统是 64 位操作系统，但应用程序以 32 位模式工作。 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 安装不支持 WOW64。 但是，WOW64 支持管理工具。  
  
 **操作系统支持：**  
  
 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 版本可划分为以下几个类别：  
  
-   [主要版本](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [扩展版本](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
> [!NOTE]  
>  以下适用于 SQL Server 2016 及更低版本的商业智能功能是此部分中所述操作系统支持的例外情况，可以在 Windows Server 2008 R2 SP1 或更高版本上安装它们：  
>  
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint  
> 
>-   用于 SharePoint 产品的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序  
  
### <a name="features-supported-on-32-bit-client-operating-systems"></a>32 位客户端操作系统支持的功能  
 Windows 客户端操作系统，例如 Windows 10 和 Windows 8.1 可作为 32 位或 64 位体系结构。   64 位客户端操作系统支持所有 SQL Server 功能。 在支持的 32 位客户端操作系统上，Microsoft 支持以下功能︰  
  
-   数据质量客户端  
  
-   客户端工具连接  
  
-   Integration Services  
  
-   客户端工具向后兼容性  
  
-   客户端工具 SDK  
  
-   文档组件  
  
-   Distributed Replay 组件  
  
-   Distributed Replay 控制器  
  
-   Distributed Replay 客户端  
  
-   SQL 客户端连接 SDK  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 和更高版本的服务器操作系统不可用作 32 位体系结构。 所有支持的服务器操作系统只可用作 64 位体系结构。 64 位服务器操作系统支持所有功能。  
  
###  <a name="TOP_Principal"></a>[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的主体版本  
 下表显示了针对 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]的主体版本的操作系统要求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|支持的操作系统|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 家庭版<br/><br/> Windows 10 专业版<br/><br/> Windows 10 企业版<br/><br/>Windows 10 IoT 企业版<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
  
\*[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支持。
  
###  <a name="TOP_Breadth"></a>[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的扩展版本  
 下表显示了针对 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]的延伸版本的操作系统要求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|支持的操作系统|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 家庭版<br/><br/> Windows 10 专业版<br/><br/> Windows 10 企业版<br/><br/>Windows 10 IoT 企业版<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 家庭版<br/><br/> Windows 10 专业版<br/><br/> Windows 10 企业版<br/><br/>Windows 10 IoT 企业版<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  

\*[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支持。
  
##  <a name="CrossLanguageSupport"></a> 跨语言支持  
 有关跨语言支持和以本地化语言安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的注意事项的详细信息，请参阅 [SQL Server 中的本地语言版本](../../sql-server/install/local-language-versions-in-sql-server.md)。  
  
##  <a name="HardDiskSpace"></a> 硬盘空间要求  
 在安装 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]的过程中，Windows Installer 会在系统驱动器中创建临时文件。 在运行安装程序以安装或升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，请检查系统驱动器中是否有至少 6.0 GB 的可用磁盘空间用来存储这些文件。 即使在将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件安装到非默认驱动器中时，此项要求也适用。  
  
 实际硬盘空间需求取决于系统配置和您决定安装的功能。 下表提供了 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 各组件对磁盘空间的要求。  
  
|**功能**|**磁盘空间要求**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 和数据文件、复制、全文搜索以及 Data Quality Services|1480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] （如上所示）带有 R Services（数据库内）|2744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] （如上所示）带有针对外部数据的 PolyBase 查询服务|4194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和数据文件|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] （独立）|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1203 MB|  
|用于 SharePoint 产品的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint Products|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|客户端工具连接|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|客户端组件（除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书组件和 Integration Services 工具之外）|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|用于查看和管理帮助内容的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书组件*|27 MB|  
|所有功能|8030 MB|  
  
 *下载的联机丛书内容需要 200 MB 的磁盘空间。  
  
##  <a name="StorageTypes"></a> 数据文件的存储类型  
 支持的数据文件存储类型包括：  
  
-   本地磁盘  
  
-   共享存储  

-   [存储空间直通 \(S2D\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)
  
-   SMB 文件共享  
  
    > [!NOTE]  
    >  无论是独立安装还是群集安装， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据文件均不支持 SMB 存储。 请改用直接连接的存储、存储区域网络或 S2D。  
  
    > [!IMPORTANT]  
    >  SMB 存储可由 Windows 文件服务器或第三方 SMB 存储设备承载。 如果使用 Windows 文件服务器，该 Windows 文件服务器版本应为 2008 或更高。 有关将 SMB 文件共享作为存储选项安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的详细信息，请参阅 [SMB 文件共享用作存储选项时安装 SQL Server](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)。  
  
    > [!WARNING]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集安装只支持使用本地磁盘安装 tempdb 文件。 确保为 tempdb 数据和日志文件指定的路径在所有群集节点上均有效。 在故障转移期间，如果 tempdb 目录对故障转移目标节点不可用，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源将无法联机。  
  
##  <a name="DC_support"></a>在域控制器上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 出于安全方面的考虑，我们建议您不要将 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 安装在域控制器上。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不会阻止在作为域控制器的计算机上进行安装，但存在以下限制：  
  
-   在域控制器上，无法在本地服务帐户下运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
-   将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装到计算机上之后，无法将此计算机从域成员更改为域控制器。 必须先卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后才能将主机计算机更改为域控制器。  
  
-   将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装到计算机上之后，无法将此计算机从域控制器更改为域成员。 必须先卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后才能将主机计算机更改为域成员。  
  
-   在群集节点用作域控制器的情况下，不支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例。  
  
- 只读域控制器不支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不能在只读域控制器上创建安全组或设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户。 在这种情况下，安装将失败。  

- 在仅可以访问只读域控制器的环境中不支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例。 
  
## <a name="see-also"></a>另请参阅  
 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)   
 [安装 SQL Server 的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [SQL Server 2016 的产品规格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
  
  

