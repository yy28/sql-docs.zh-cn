---
title: 安装 SQL Server 2014 的硬件和软件要求 |Microsoft Docs
ms.custom: ''
ms.date: 07/10/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce6cef69abe7c2461552229363c8334ca56555b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245656"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server-2014"></a>Hardware and Software Requirements for Installing SQL Server 2014

 > - 安装**[免费的开发人员版](https://my.visualstudio.com/Downloads?q=SQL%20Server%20Developer)，尝试 SQL Server 2016！**  
  
## <a name="considerations"></a>注意事项 
  
-   建议在 NTFS [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]文件格式的计算机上运行。 支持 FAT32 文件系统，但不建议这样做，因为它不如 NTFS 文件系统安全。  
  
-   不能在只读驱动器、映射的驱动器或压缩驱动器上安装。  
  
-   若要允许 Visual Studio 组件正确安装， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要安装更新。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序会检查此更新是否存在，然后要求您先下载并安装该更新，然后才能继续[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装。 若要避免在安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]过程中中断，请**在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序之前**下载并安装此更新，如下所述（或安装 WINDOWS 更新上提供的 .net 3.5 SP1 的所有更新）：  
  
    -   对于[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2，请在[此处](https://go.microsoft.com/fwlink/?LinkId=198093)获取所需的更新。  
  
    -   对于任何其他受支持的操作系统，都包括此更新。  
  
-   不支持通过 Terminal Services Client 启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。 如果通过 "终端服务客户端" 启动安装程序，安装将失败。   
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序安装该产品所需的以下软件组件：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client{2}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序支持文件  
  
-   有关在或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[win8srv](../../includes/win8srv-md.md)] [!INCLUDE[win8](../../includes/win8-md.md)]上安装的最低版本要求，请参阅[在 Windows Server 2012 或 windows 8 上安装 SQL Server](https://support.microsoft.com/kb/2681562) （https://support.microsoft.com/kb/2681562)。  
  
 本主题包含以下各节：  
  
-   [硬件和软件要求](hardware-and-software-requirements-for-installing-sql-server.md#hwswr)  
  
-   [处理器、内存和操作系统要求](hardware-and-software-requirements-for-installing-sql-server.md#pmosr)  
  
-   [跨语言支持](hardware-and-software-requirements-for-installing-sql-server.md#CrossLanguageSupport)  
  
-   [扩展系统支持](hardware-and-software-requirements-for-installing-sql-server.md#ess)  
  
-   [硬盘空间要求（32 位和 64 位）](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)  
  
-   [数据文件的存储类型](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)  
  
-   [在域控制器上安装 SQL Server](hardware-and-software-requirements-for-installing-sql-server.md#DC_support)  
  
##  <a name="hwswr"></a>硬件和软件要求  
 以下要求适用于所有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装：  
  
|组件|要求|  
|---------------|-----------------|  
|.NET Framework|在选择 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、复制或 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]时，.NET 3.5 SP1 是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]所必需的，但不再由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序安装。 <br />-如果您运行安装程序但没有 .NET 3.5 SP1，则安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]程序将要求您先下载并安装 .NET 3.5 sp1，然后才能继续[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装。 （从[Microsoft .NET Framework 3.5 Service Pack 1](https://www.microsoft.com/download/details.aspx?id=22)安装 .NET 3.5 SP1。）错误消息中包含指向下载中心的链接，也可从 Windows 更新下载 .NET 3.5 SP1。 若要避免在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装期间中断，可在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序之前，先下载并安装 .NET 3.5 SP1。<br />-如果在安装了[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 或[!INCLUDE[win8](../../includes/win8-md.md)]的计算机上运行安装程序，则必须先启用 .NET Framework 3.5 SP1 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，然后再安装。<br />-如果没有 internet 访问，则必须在运行安装程序之前下载并安装 .NET Framework 3.5 SP1，才能安装以上提到的任何组件。 有关如何获取和[!INCLUDE[win8](../../includes/win8-md.md)]启用和[!INCLUDE[win8srv](../../includes/win8srv-md.md)]的 .NET Framework 3.5 的建议和指南的详细信息，请参阅[Microsoft .NET Framework 3.5 部署注意事项](https://msdn.microsoft.com/library/windows/hardware/hh975396)（。https://msdn.microsoft.com/library/windows/hardware/hh975396)<br /><br /> .NET 4.0 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]所必需的。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在功能安装步骤中安装 .NET 4.0。<br />-如果要安装[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]版本，请确保 Internet 连接在计算机上可用。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将下载并安装 .NET Framework 4，因为 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 介质不包含该软件。<br />-[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]不会在[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 或[!INCLUDE[win8srv](../../includes/win8srv-md.md)]的服务器核心模式上安装 .net 4.0。 您必须首先安装 .NET 4.0，然后才能在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] SP1 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安装上安装 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]。|  
|Windows PowerShell|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不安装或启用 Windows PowerShell 2.0；但对于[!INCLUDE[ssDE](../../includes/ssde-md.md)]组件和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 而言，Windows PowerShell 2.0 是一个安装必备组件。 如果安装程序报告缺少 Windows PowerShell 2.0，您可以按照 [Windows 管理框架](https://go.microsoft.com/fwlink/?LinkId=186214) 页中的说明安装或启用它。|  
|网络软件|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持的操作系统具有内置网络软件。 独立安装的命名实例和默认实例支持以下网络协议：共享内存、命名管道、TCP/IP 和 VIA。<br /><br /> 注意：故障转移群集上不支持 VIA 协议。 与 SQL Server 实例在同一故障转移群集节点上运行的客户端或应用程序可以使用 Shared Memory 协议，通过其本地管道地址连接到 SQL Server。 不过，这种连接无法感知群集，因此会在实例故障转移后无法连接。 因此，不建议使用这种连接，只能用于极个别的方案。 不推荐使用 VIA 协议。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> 有关网络协议和网络库的详细信息，请参阅 [Network Protocols and Network Libraries](network-protocols-and-network-libraries.md)。|  
|虚拟化|在以下版本中以 Hyper-V 角色运行的虚拟机环境中支持 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]：<br />-<br />                    
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard、Enterprise 和 Datacenter 版本<br />-[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard、Enterprise 和 Datacenter 版本。<br />-<br />                    
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 和 Standard 版本。<br /><br /> 除了父分区所需的资源以外，还必须为每个虚拟机（子分区）的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例提供足够的处理器资源、内存和磁盘资源。 具体要求在本主题的后面章节中列出。\*<br /><br /> 在 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 上的 Hyper-V 角色中，最多可以为运行 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 32 位/64 位、 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 位版本的虚拟机分配 4（四）个虚拟处理器。<br /><br /> 在上[!INCLUDE[win8srv](../../includes/win8srv-md.md)]的 hyper-v 角色中：<br />最多可以为运行 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 32 位/64 位的虚拟计算机分配 8（八）个虚拟处理器。<br />最多可以为运行 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 位版本的虚拟机分配 64（六十四）个虚拟处理器。<br /><br /> 若要详细了解不同版本的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]计算容量限制以及它们在物理环境和虚拟化环境中与超线程处理器的区别，请参阅[按版本 SQL Server 计算容量限制](../compute-capacity-limits-by-edition-of-sql-server.md)。 有关 Hyper-V 角色的详细信息，请参阅 [Windows Server 2008 网站](https://go.microsoft.com/fwlink/?LinkId=182820)。<br /><br /> ** \* \*重要\*提示**中[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]支持来宾故障转移群集。 有关用于来宾故障转移群集的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和操作系统的支持版本的详细信息以及对虚拟化的支持的详细信息，请参阅 [针对在硬件虚拟环境中运行的 Microsoft SQL Server 产品的支持策略](https://go.microsoft.com/fwlink/?LinkId=151676)。|  
|硬盘|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 要求最少 6 GB 的可用硬盘空间。<br /><br /> 磁盘空间要求将随所安装的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 组件不同而发生变化。 有关详细信息，请参阅本主题后面的 [Hard Disk Space Requirements (32-Bit and 64 Bit)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) 。 有关支持的数据文件存储类型的信息，请参阅 [Storage Types for Data Files](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)。|  
|驱动器|从磁盘进行安装时需要相应的 DVD 驱动器。|  
|监视|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 要求有 Super-VGA (800x600) 或更高分辨率的显示器。|  
|Internet|使用 Internet 功能需要连接 Internet（可能需要付费）。|  
  
 * 在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]虚拟机上运行的速度要慢于在本机运行，因为虚拟化会产生系统开销。  
  
##  <a name="pmosr"></a>处理器、内存和操作系统要求  
 以下内存和处理器要求适用于所有版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]：  
  
|组件|要求|  
|---------------|-----------------|  
|内存<sup>[1]</sup>|**短**<br /><br /> Express 版本：512 MB<br /><br /> 所有其他版本：1 GB<br /><br /> **您**<br /><br /> Express 版本：1 GB<br /><br /> 所有其他版本：至少 4 GB 并且应该随着数据库大小的增加而增加，以便确保最佳的性能。|  
|处理器速度|**短**<br /><br /> x86 处理器：1.0 GHz<br /><br /> x64 处理器：1.4 GHz<br /><br /> **建议：** 2.0 GHz 或更快|  
|处理器类型|x64 处理器：AMD Opteron、AMD Athlon 64、支持 Intel EM64T 的 Intel Xeon、支持 EM64T 的 Intel Pentium IV<br /><br /> x86 处理器：Pentium III 兼容处理器或更快|  
  
 <sup>[1]</sup>在（DQS）中[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]安装组件所需的最小内存是 2 GB 的 RAM，这不同于[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]最小内存要求。 有关安装 DQS 的信息，请参阅 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
 **WOW64 支持：**  
  
 WOW64（Windows 64 位上的 Windows 32 位）是 Windows 64 位版本中的一项功能，使用该功能可以在 32 位模式下本机运行 32 位应用程序。 尽管基础操作系统是 64 位操作系统，但应用程序以 32 位模式工作。  
  
-   在支持的 64 位操作系统上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 位版本可以安装到 64 位服务器的 WOW64 32 位子系统中。 仅对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的独立实例才支持 WOW64。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集安装不支持 WOW64。  
  
-   对于在支持的 64 位操作系统上安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 位版本，WOW64 中支持管理工具。 有关支持的操作系统的详细信息，请在下面各节中选择 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的版本。  
  
 **服务器核心支持：**  

 Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 和 Windows Server 2019 的 Server Core 中现在支持安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 

以下 Windows Server 版本支持在 Server Core 模式上安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ：

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2 Datacenter|
| Windows Server 2012 Standard | Windows Server 2012 Datacenter |
| Windows Server 2008 R2 SP1 Standard | Windows Server 2008 R2 SP1 Datacenter |
| Windows Server 2008 R2 SP1 Enterprise | Windows Server 2008 R2 SP1 Web|
   | &nbsp; | &nbsp; |
  
 有关在 Server Core 上[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装的详细信息，请参阅在[Server core 上安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server-on-server-core.md)。  
  
   >[!NOTE]
   > 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 位 x64 Standard 版本中支持的 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 版本在 [!INCLUDE[sbs_2](../../includes/sbs-2-md.md)] 64 位 x64 版本中也受支持。  
  
 **操作系统支持：**  
  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本可划分为以下几个类别：  
  
-   [SQL Server 2014 的主要版本](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [SQL Server 2014 专业版](hardware-and-software-requirements-for-installing-sql-server.md#TOP_SP)  
  
-   [SQL Server 2014 的延伸版本](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
###  <a name="TOP_Principal"></a>主体版本操作系统要求  
 下表显示了针对 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的主体版本的操作系统要求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本|32 位|64 位|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 标准32位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Business Intelligence{2}|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 标准32位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|Windows 10 家庭版 64 位<br /><br /> Windows 10 专业版 64 位<br /><br /> Windows 10 企业版 64 位<br /><br /> Windows 10 家庭版 32 位<br /><br /> Windows 10 专业版 32 位<br /><br /> Windows 10 企业版 32 位<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 标准32位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位|Windows 10 家庭版 64 位<br /><br /> Windows 10 专业版 64 位<br /><br /> Windows 10 企业版 64 位<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位| 
  
###  <a name="TOP_SP"></a>专用版本操作系统要求  
 下表显示了针对 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的专业版本的操作系统要求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本|32 位|64 位|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|Windows 10 家庭版 64 位<br /><br /> Windows 10 专业版 64 位<br /><br /> Windows 10 企业版 64 位<br /><br /> Windows 10 家庭版 32 位<br /><br /> Windows 10 专业版 32 位<br /><br /> Windows 10 企业版 32 位<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 标准32位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位|Windows 10 家庭版 64 位<br /><br /> Windows 10 专业版 64 位<br /><br /> Windows 10 企业版 64 位<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位| 
  
###  <a name="TOP_Breadth"></a>广度版本操作系统要求
 下表显示了针对 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的延伸版本的操作系统要求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本|32 位|64 位|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|Windows 10 家庭版 64 位<br /><br /> Windows 10 专业版 64 位<br /><br /> Windows 10 企业版 64 位<br /><br /> Windows 10 家庭版 32 位<br /><br /> Windows 10 专业版 32 位<br /><br /> Windows 10 企业版 32 位<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 标准32位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位|Windows 10 家庭版 64 位<br /><br /> Windows 10 专业版 64 位<br /><br /> Windows 10 企业版 64 位<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|Windows 10 家庭版 64 位<br /><br /> Windows 10 专业版 64 位<br /><br /> Windows 10 企业版 64 位<br /><br /> Windows 10 家庭版 32 位<br /><br /> Windows 10 专业版 32 位<br /><br /> Windows 10 企业版 32 位<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 32 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 标准32位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位|Windows 10 家庭版 64 位<br /><br /> Windows 10 专业版 64 位<br /><br /> Windows 10 企业版 64 位<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 标准64位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 位|  
  
## <a name="minimum-sql-server-version-requirements-for-windows-10"></a>适用于 Windows 10 的最低 SQL Server 版本要求  
 在运行 Windows 10 的计算机上安装 SQL Server 之前，必须确保满足以下最低要求：  
  
-   对于 SQL Server 2014，必须应用 SQL Server 2014 Service Pack 1 或更高版本的更新。 有关详细信息，请参阅 [如何获取 SQL Server 2014 的最新 Service Pack](https://support.microsoft.com/kb/2958069)。  
  
-   对于 SQL Server 2012，必须应用 SQL Server 2012 Service Pack 2 或更高版本的更新。 有关详细信息，请参阅 [如何获取 SQL Server 2012 的最新 Service Pack](https://support.microsoft.com/kb/2755533)。  
  
-   SQL Server 2008 R2  
    Windows 10 不支持和 SQL Server 2008。  
  
##  <a name="CrossLanguageSupport"></a>跨语言支持  
 有关跨语言支持和以本地化语言安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的注意事项的详细信息，请参阅 [SQL Server 中的本地语言版本](local-language-versions-in-sql-server.md)。  
  
##  <a name="ess"></a>扩展系统支持  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 位版本支持扩展系统，也称作“Windows 64 位上的 Windows 32 位 (WOW64)”。 WOW64 是 Windows 64 位版本中的一个功能，使用该功能可以以 32 位模式在本机执行 32 位应用程序。 尽管基础操作系统是 64 位，但应用程序以 32 位模式工作。  
  
##  <a name="HardDiskSpace"></a>硬盘空间要求（32位和64位）  
 在安装过程中 Windows Installer 在系统驱动器上创建临时文件。 在运行安装程序以安装或升级[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，请确保系统驱动器上至少有**6.0 GB**的可用磁盘空间用于这些文件。 即使将组件安装到非默认驱动器，此要求也适用。  
  
 实际硬盘空间需求取决于系统配置和您决定安装的功能。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 下表提供了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 各组件对磁盘空间的要求。  
  
|**功能**|**磁盘空间要求**|  
|-----------------|--------------------------------|  
|
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和数据文件、复制、全文搜索以及 Data Quality Services|811 MB|  
|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和数据文件|345 MB|  
|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和报表管理器|304 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|591 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|243 MB|  
|客户端组件（除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书组件和 Integration Services 工具之外）|1823 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于查看和管理帮助内容的联机丛书组件<sup>1</sup>|375 KB|  
  
 <sup>1</sup>下载的联机丛书内容的磁盘空间要求为 200 MB。  
  
##  <a name="StorageTypes"></a>数据文件的存储类型  
 支持的数据文件存储类型包括：  
  
-   本地磁盘  
  
-   共享存储  
  
-   SMB 文件共享  
  
    > **注意：** 对于独立安装或群集安装[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，数据文件不支持 SMB 存储。 请改用直接连接存储或存储区域网络。  
  
    > **重要说明!!** SMB 存储可由 Windows 文件服务器或第三方 SMB 存储设备承载。 如果使用 Windows 文件服务器，该 Windows 文件服务器版本应为 2008 或更高。 有关将 SMB 文件共享作为存储选项安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的详细信息，请参阅 [SMB 文件共享用作存储选项时安装 SQL Server](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)。  
  
    > **警告!!!!**  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集安装只支持使用本地磁盘安装 tempdb 文件。 确保为 tempdb 数据和日志文件指定的路径在**所有**群集节点上都有效。 在故障转移期间，如果 tempdb 目录对故障转移目标节点不可用，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源将无法联机。  
  
##  <a name="DC_support"></a>在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]域控制器上安装-限制  
 出于安全方面的考虑，我们建议您不要将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装在域控制器上。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不会阻止在作为域控制器的计算机上进行安装，但存在以下限制：  
  
-   在域控制器上，无法在本地服务帐户下运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
-   将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装到计算机上之后，无法将此计算机从域成员更改为域控制器。 必须先卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后才能将主机计算机更改为域控制器。  
  
-   将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装到计算机上之后，无法将此计算机从域控制器更改为域成员。 必须先卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后才能将主机计算机更改为域成员。  
  
-   在群集节点用作域控制器的情况下，不支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例。  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不能在只读域控制器上创建安全组或设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户。 在这种情况下，安装将失败。  
  
## <a name="see-also"></a>另请参阅  
 [计划 SQL Server 安装](planning-a-sql-server-installation.md)   
 [安装 SQL Server 的安全注意事项](security-considerations-for-a-sql-server-installation.md)   
 [SQL Server 2014 的产品规格](../../getting-started/sql-server-2014-product-specifications.md)  
