---
title: 获取和配置加载服务器的并行数据仓库 |Microsoft Docs
description: 本文介绍如何获取和将加载服务器配置为用于提交数据加载到并行数据仓库 (PDW) 的非设备 Windows 系统。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da404aa881f3ff7af26a681751aae12a45f2628f
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703775"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>获取和并行数据仓库配置加载服务器
本文介绍如何获取和将加载服务器配置为用于提交数据加载到并行数据仓库 (PDW) 的非设备 Windows 系统。  
  
## <a name="Basics"></a>基础知识  
加载服务器中：  
  
-   没有为一台服务器。 您可以与多个加载服务器同时加载。  
  
-   提供并由 IT 团队管理。 你可能已在服务器或可用于将数据加载到 PDW 的服务器。  
  
-   位于您自己的非设备机架，且不能放置在分析平台系统 appliance。  
  
-   连接到设备通过设备 InfiniBand 网络，或通过以太网。 为了性能，我们建议使用 InfiniBand。  
  
-   是在您自己客户域中，不是在设备域。 客户域的设备域之间没有信任关系。  
  
## <a name="Step1"></a>步骤 1： 确定容量要求  
正在加载系统可以设计为执行并发负载的一个或多个加载服务器。 加载的每个服务器不必专用于加载，，只要它将处理工作负荷的性能和存储要求。  
  
加载服务器的系统要求几乎完全取决于自己的工作负荷。 使用[加载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)以帮助确定容量要求。  
  
## <a name="Step2"></a>步骤 2： 获取 sServer  
现在，更好地了解你的容量要求，您可以计划的服务器和网络将需要购买或预配的组件。 将下面的要求列表合并到你购买的计划，然后购买你的服务器或预配的现有服务器。  
  
### <a name="R"></a>软件要求  
支持的操作系统：  
  
-   Windows Server 2012 或 Windows Server 2012 R2。 这些操作系统的系统要求以 FDR 网络适配器。  
  
-   Windows Server 2008 R2。 此 OS 需要 DDR 网络适配器。  
  
服务器必须使用 EN-US 区域设置，才能使用 dwloader 命令行加载工具。 dwloader 不支持其他区域设置。  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Windows Server 2012 和 Windows Server 2012 R2 的网络要求  
尽管不需要加载，无限带宽是建议的连接类型用于加载服务器。 为了获得最佳性能，使用 Windows Server 2012 或 Windows Server 2012 R2 和 FDR InfiniBand 网络适配器将加载服务器连接到设备 InfiniBand 网络。  
  
若要准备的 Windows Server 2012 或 Windows Server 2012 R2 InfiniBand 连接：  
  
1.  计划安装机架服务器关闭足够到设备，以便可以将其连接到 InfiniBand 切换的设备。 有关 InfiniBand 从 Mellanox 技术的详细信息，请参阅白皮书[简介 InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  购买 Mellanox ConnectX 3 FDR InfiniBand 单或双端口的网络适配器。 我们建议在数据传输过程中购买的容错能力的两个端口的网络适配器。 为实现高可用性需要两个端口网络适配器。  
  
3.  购买 2 个 FDR InfiniBand 电缆双端口卡片或为单个端口卡 1 FDR InfiniBand 网络。 FDR InfiniBand 电缆将连接到设备 InfiniBand 网络加载服务器。 电缆长度取决于加载服务器和设备 InfiniBand 交换机之间的距离根据您的环境。  
  
## <a name="Step3"></a>步骤 3： 将服务器连接到 InfiniBand 网络  
使用以下步骤将加载服务器连接到 InfiniBand 网络。 如果服务器不使用 InfiniBand 网络，请跳过此步骤。  
  
1.  机架服务器得足够近到设备，以便可以将其连接到设备 InfiniBand 网络。  
  
2.  将 InfiniBand Mellanox ConnectX 3 FDR InfiniBand 网络适配器安装到加载服务器。  
  
3.  使用以 FDR 电缆 InfiniBand 网络适配器连接到第一个设备机架中的两个 InfiniBand 开关之一。  
  
4.  安装和配置 InfiniBand 网络适配器的相应 Windows 驱动程序。  
  
    -   Windows 的 InfiniBand 驱动程序开发的 OpenFabrics 联盟的 InfiniBand 供应商。  使用 InfiniBand 网络适配器中，可能已分发的正确驱动程序。 如果没有，可以从 www.openfabrics.org 下载驱动程序。  
  
5.  配置网络适配器的 InfiniBand 和 DNS 设置。 有关配置说明，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。  
  
## <a name="Step4"></a>步骤 4： 安装的加载工具  
客户端工具均可从 Microsoft 下载中心下载。 

若要安装 dwloader，请从客户端工具运行 dwloader 安装。
  
如果你打算使用适用于加载的 Integration Services，您需要安装 Integration Services 和 Integration Services 目标适配器。 适配器是客户端工具中提供。

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>步骤 5： 启动加载  
现在您就可以开始加载数据。 有关详细信息，请参阅：  
  
1.  [dwloader 命令行加载工具](dwloader.md)  
  
2.  [加载概述](load-overview.md)  
  
## <a name="performance"></a>“性能”  
最佳加载性能在 Windows Server 2012 和更高版本，启用即时文件初始化，以便数据覆盖时，操作系统将不会覆盖现有数据用零。 如果这是存在安全风险，因为之前的数据仍存在于磁盘上，然后务必关闭即时文件初始化。  
  
## <a name="Security"></a>安全通知  
由于要加载的数据不存储在设备上，你的 IT 团队负责管理为你要加载的数据安全性的各个方面。 例如，这包括管理要加载的数据的安全性、 用来存储负载的服务器的安全和将加载服务器连接到 SQL Server PDW 设备的网络基础结构的安全性。  
  
> [!IMPORTANT]  
> 尤其是务必保护将使用 dwloader 命令行加载工具的每个加载服务器。 当 dwloader 加载数据时，它首先进行身份验证与控制节点，并将身份验证成功后移动的数据从加载服务器直接到计算节点通过数据通道。 证书验证期间加载的每个服务器和每个计算节点之间的手抖动不会发生。 这将使人为干预发动攻击时加载每个数据通道上公开的计算节点。 这些攻击可能导致信息泄露和/或被篡改的数据。  
  
若要减少你的数据的安全风险，我们建议：  
  
-   将指定一个专门用于将数据加载到 PDW 所使用的 Windows 帐户。 允许此帐户有权加载位置和其他位置不可用。  
  
-   将指定一个有权加载数据的 PDW 用户。 具体取决于您的安全要求，你可以每个数据库的一个特定用户。  
  
-   加载服务器上的操作可以接受 UNC 路径从其提取数据从受信任的内部网络之外。 和在网络上或能够影响名称解析攻击者可以截获或更改数据发送到 SQL Server PDW。 这带来篡改和信息泄露的风险。 应通过要求在连接上签名缓解篡改。 若要帮助缓解此风险，设置以下组策略选项**Security Settings\Local Policies\Security Options**加载服务器上： **Microsoft 网络客户端： 数字签名通信 （始终）：已启用**  
  
-   关闭 Windows Server 2012 和更高版本的即时文件初始化。 在性能部分中所述，这是性能和安全性之间的权衡。 您需要确定什么最根据您的安全要求。  
  
## <a name="see-also"></a>请参阅  
[备份和还原概述](backup-and-restore-overview.md)  
  
