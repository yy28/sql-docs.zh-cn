---
title: 获取和配置加载服务器-并行数据仓库 |Microsoft 文档
description: 本文介绍如何获取和将加载服务器配置为非设备 Windows 系统用于提交数据加载到并行数据仓库 (PDW)。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a796616ad76ba62ea4174cf22c1517c489305055
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538987"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>获取和并行数据仓库的配置加载服务器
本文介绍如何获取和将加载服务器配置为非设备 Windows 系统用于提交数据加载到并行数据仓库 (PDW)。  
  
## <a name="Basics"></a>基础知识  
加载服务器中：  
  
-   没有为单个服务器。 你可以与多个加载服务器同时加载。  
  
-   提供和由你自己的 IT 团队。 你可能已可用于将数据加载到 PDW 的服务器或的服务器。  
  
-   位于你自己的非设备机架，并且不能放置在分析平台系统设备。  
  
-   连接到设备通过设备 InfiniBand 网络中，或通过以太网。 为性能，我们建议使用无限带宽。  
  
-   是在你自己客户域中，不是在设备域。 客户域和设备的域之间没有信任关系。  
  
## <a name="Step1"></a>步骤 1： 确定容量要求  
加载系统可以设计为一个或多个执行并发加载的加载服务器。 加载的每个服务器不必专用于加载，，只要它将处理你的工作负荷的性能和存储要求。  
  
加载服务器的系统要求几乎完全取决于你自己的工作负荷。 使用[加载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)以帮助确定你的容量要求。  
  
## <a name="Step2"></a>步骤 2： 获取 sServer  
现在，你更好地了解你的容量要求，你可以计划的服务器和网络将需要购买，也可以设置的组件。 将下面列出的要求合并到你购买的计划，然后购买你的服务器或配置现有服务器。  
  
### <a name="R"></a>软件要求  
支持的操作系统：  
  
-   Windows Server 2012 或 Windows Server 2012 R2。 这些操作系统的系统要求 FDR 网络适配器。  
  
-   Windows Server 2008 R2。 此操作系统需要 DDR 网络适配器。  
  
服务器必须使用 EN-US 区域设置，才能使用 dwloader 加载命令行工具。 dwloader 不支持其他区域设置。  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Windows Server 2012 和 Windows Server 2012 R2 的网络要求  
尽管无需进行加载，则无限带宽是建议的连接类型用于加载服务器。 为了获得最佳性能，使用 Windows Server 2012 或 Windows Server 2012 R2 和 FDR InfiniBand 网络适配器将加载服务器连接到设备 InfiniBand 网络。  
  
若要准备的 Windows Server 2012 或 Windows Server 2012 R2 InfiniBand 连接：  
  
1.  计划机架服务器关闭足够到设备，以便你可以将其连接到设备 InfiniBand 切换。 有关 InfiniBand 和 Mellanox 技术的详细信息，请参阅白皮书，[简介 InfiniBand](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  购买 Mellanox connectx-3 FDR InfiniBand 单或双端口的网络适配器。 我们建议在数据传输过程购买容错功能的两个端口的网络适配器。 为实现高可用性需要两个端口的网络适配器。  
  
3.  购买 2 FDR InfiniBand 条电缆，用于双端口卡或为单个端口卡 1 FDR InfiniBand 电缆。 FDR InfiniBand 电缆将连接到设备 InfiniBand 网络加载服务器。 电缆长度取决于在加载服务器和设备 InfiniBand 交换机之间的距离根据你的环境。  
  
## <a name="Step3"></a>步骤 3： 将服务器连接到的 InfiniBand 网络  
使用这些步骤将加载服务器连接到的 InfiniBand 网络。 如果服务器未使用 InfiniBand 网络，跳过此步骤。  
  
1.  机架服务器足够近到设备，以便你可以将其连接到的设备 InfiniBand 网络。  
  
2.  将 InfiniBand Mellanox connectx-3 FDR InfiniBand 网络适配器安装到加载服务器。  
  
3.  使用 FDR 电缆 InfiniBand 网络适配器连接到第一个设备机架中的两个 InfiniBand 开关之一。  
  
4.  安装和配置适当 Windows InfiniBand 网络适配器驱动程序。  
  
    -   适用于 Windows InfiniBand 驱动程序是通过 OpenFabrics 联盟，InfiniBand 供应商行业联合会开发的。  正确的驱动程序可能已与你 InfiniBand 网络适配器中分发。 如果没有，可以从 www.openfabrics.org 下载驱动程序。  
  
5.  配置网络适配器的 InfiniBand 和 DNS 设置。 有关配置说明，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。  
  
## <a name="Step4"></a>步骤 4： 安装的加载工具  
客户端工具均可供从 Microsoft 下载中心下载。 

若要安装 dwloader，请从客户端工具运行 dwloader 安装。
  
如果你打算使用加载的 Integration Services，你将需要安装 Integration Services 和 Integration Services 目标适配器。 适配器为客户端工具中提供。

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>步骤 5： 启动加载  
现在你就可以开始加载数据。 有关详细信息，请参阅：  
  
1.  [dwloader 命令行加载工具](dwloader.md)  
  
2.  [负载概述](load-overview.md)  
  
## <a name="performance"></a>性能  
加载性能上 Windows Server 2012 和更高版本的最佳，开启即时文件初始化，以便数据覆盖时，操作系统将不会覆盖现有数据用零。 如果这是安全风险，因为以前的数据仍存在于磁盘上，然后务必关闭即时文件初始化。  
  
## <a name="Security"></a>安全声明  
由于要加载的数据不存储在设备上，你的 IT 团队负责管理您的数据以加载的安全性的所有方面。 例如，这包括管理要加载的数据的安全性、 用来存储负载的服务器的安全性和将加载服务器连接到 SQL Server PDW 设备的网络基础结构的安全性。  
  
> [!IMPORTANT]  
> 尤其是，务必确保每个将使用 dwloader 加载命令行工具的加载服务器的安全。 当 dwloader 加载数据时，它首先使用进行身份验证的控件节点，并将身份验证成功后它移动数据从加载服务器直接到计算节点对数据通道。 加载的每个服务器和每个计算节点之间的现有动摇期间未出现证书验证。 这将使计算节点容易遭受时加载每个数据通道上的潜在拦截的攻击。 这些攻击可能导致篡改过的数据和/或信息泄露。  
  
若要减少与你的数据的安全风险，我们建议以下各项：  
  
-   指定一个使用专门用于将数据加载到 PDW 的 Windows 帐户。 允许此帐户有权加载位置和其他地方。  
  
-   将指定有权加载数据的一个 PDW 用户。 具体取决于您的安全要求，你可以每个数据库的一个特定用户。  
  
-   加载服务器上的操作可以接受从中提取数据从受信任的内部网络之外的 UNC 路径。 而攻击者在网络上还是能够影响名称解析可以截获或修改数据发送到 SQL Server PDW。 这存在篡改和信息泄露风险。 应通过要求在连接登录缓解篡改。 为了帮助减轻这种风险，在中设置以下组策略选项**安全设置 \ 本地策略 \ 安全选项**加载服务器上： **Microsoft 网络客户端： 数字签名通信 （始终）：启用**  
  
-   关闭 Windows Server 2012 上和更高版本的即时文件初始化。 在性能部分中所述，这是性能和安全性之间的权衡。 你需要决定什么是最佳根据您的安全要求。  
  
## <a name="see-also"></a>另请参阅  
[备份和还原概述](backup-and-restore-overview.md)  
  
