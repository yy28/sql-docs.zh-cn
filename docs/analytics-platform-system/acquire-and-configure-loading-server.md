---
title: 获取 & 配置加载服务器
description: 本文介绍如何将加载服务器作为非设备 Windows 系统获取和配置，以便将数据加载到并行数据仓库（PDW）。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef49bb86c8e16600f2ff1bf2d1c7a92ecc5af964
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401479"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>为并行数据仓库获取和配置加载服务器
本文介绍如何将加载服务器作为非设备 Windows 系统获取和配置，以便将数据加载到并行数据仓库（PDW）。  
  
## <a name="Basics"></a>传授  
加载服务器：  
  
-   不必是单一服务器。 可以同时加载多个加载服务器。  
  
-   由你自己的 IT 团队提供和管理。 可能已有一个服务器或服务器可用于将数据加载到 PDW。  
  
-   位于自己的非设备机架中，不能放置在分析平台系统设备内。  
  
-   通过设备无线网络或通过以太网连接到设备。 为了提高性能，我们建议使用 "不限"。  
  
-   位于你自己的客户域中，而不是设备域。 你的客户域与设备域之间没有信任关系。  
  
## <a name="Step1"></a>步骤1：确定容量要求  
加载系统可设计为执行并发加载的一个或多个加载服务器。 每个加载服务器不必专用于加载，只要它将处理工作负荷的性能和存储要求。  
  
加载服务器的系统要求几乎完全取决于您自己的工作负载。 使用[加载服务器容量规划工作表](loading-server-capacity-planning-worksheet.md)来帮助确定容量需求。  
  
## <a name="Step2"></a>步骤2：获取 Server  
既然您更好地了解了容量要求，您可以规划需要购买或预配的服务器和网络组件。 将以下要求列表纳入购买计划，然后购买服务器或预配现有服务器。  
  
### <a name="R"></a>软件要求  
支持的操作系统：  
  
-   Windows Server 2012 或 Windows Server 2012 R2。 这些操作系统需要 FDR 网络适配器。  
  
-   Windows Server 2008 R2。 此操作系统需要 DDR 网络适配器。  
  
服务器必须使用 EN-US 区域设置，才能使用 dwloader 命令行加载工具。 dwloader 不支持其他区域设置。  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Windows Server 2012 和 Windows Server 2012 R2 的网络要求  
尽管不需要进行加载，但建议使用连接类型来加载服务器。 为了获得最佳性能，请使用 Windows Server 2012 或 Windows Server 2012 R2，并使用 FDR 的网络适配器将加载服务器连接到设备的网络设备。  
  
准备 Windows Server 2012 或 Windows Server 2012 R2 连接：  
  
1.  计划将服务器的机架接近于设备，以便可以将其连接到设备未被交换机。 若要深入了解有关不受阻止的 Mellanox 技术的详细信息，请参阅白皮书[简介](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  购买 Mellanox ConnectX-3 FDR 无限单或双端口网络适配器。 建议购买包含两个端口的网络适配器，以在数据传输期间获得容错。 需要两个端口网络适配器才能实现高可用性。  
  
3.  为双端口卡购买2个 FDR 的，或者为单端口卡购买1个 FDR 的电源线。 FDR 的无线电缆会将加载服务器连接到设备的 "无线网络"。 缆线长度取决于负载服务器与设备不会的交换机之间的距离，取决于您的环境。  
  
## <a name="Step3"></a>步骤3：将服务器连接到不工作网络  
使用以下步骤将加载服务器连接到 "未占用网络"。 如果服务器未使用 "未使用" 网络，请跳过此步骤。  
  
1.  使服务器接近于设备，以便可以将其连接到设备的 "无线网络"。  
  
2.  将不限的 Mellanox ConnectX-3 FDR 的网络适配器安装到加载服务器。  
  
3.  使用 FDR 电缆将无线网络适配器连接到第一个设备机架中的两个未被使用的交换机之一。  
  
4.  为未被配置的网络适配器安装和配置适当的 Windows 驱动程序。  
  
    -   适用于 Windows 的不受使用的驱动程序由 OpenFabrics 联盟（一种行业协会，这是一家不受人  正确的驱动程序可能已随您的 "未使用" 网络适配器一起分发。 否则，可以从 www.openfabrics.org 下载该驱动程序。  
  
5.  为网络适配器配置 "未设置" 和 "DNS" 设置。 有关配置说明，请参阅[配置无线网络适配器](configure-infiniband-network-adapters.md)。  
  
## <a name="Step4"></a>步骤4：安装加载工具  
可从 Microsoft 下载中心下载客户端工具。 

若要安装 dwloader，请从客户端工具运行 dwloader 安装。
  
如果计划使用 Integration Services 进行加载，则需要安装 Integration Services 和 Integration Services 目标适配器。 客户端工具中提供了适配器。

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>步骤5：开始加载  
你现在已准备好开始加载数据。 有关详细信息，请参阅：  
  
1.  [dwloader 命令行加载工具](dwloader.md)  
  
2.  [负载概述](load-overview.md)  
  
## <a name="performance"></a>性能  
若要在 Windows Server 2012 和更高版本中获得最佳加载性能，请打开即时文件初始化，以便在覆盖数据时，操作系统将不会用零覆盖现有数据。 如果这是安全风险，因为以前的数据仍存在于磁盘上，请确保关闭即时文件初始化。  
  
## <a name="Security"></a>安全通知  
由于要加载的数据未存储在设备上，因此你的 IT 团队负责管理要加载的数据的安全的所有方面。 例如，这包括管理要加载的数据的安全、用于存储负载的服务器的安全性，以及将加载服务器连接到 SQL Server PDW 设备的网络基础结构的安全性。  
  
> [!IMPORTANT]  
> 尤其重要的是保护将使用 dwloader 命令行加载工具的每个加载服务器。 当 dwloader 加载数据时，它首先通过控制节点进行身份验证，然后在成功完成身份验证后，它会将数据从加载服务器直接移到通过数据通道的计算节点。 不会在每个加载服务器和每个计算节点之间进行证书验证。 这会使计算节点在加载时对每个数据通道的潜在中间人攻击进行公开。 这些攻击可能会导致篡改的数据和/或信息泄露。  
  
为了降低数据的安全风险，我们建议执行以下操作：  
  
-   指定一个专门用于将数据加载到 PDW 的 Windows 帐户。 允许此帐户具有加载位置的权限。  
  
-   指定一个有权加载数据的 PDW 用户。 根据您的安全要求，每个数据库都有一个特定的用户。  
  
-   加载服务器上的操作可以接受 UNC 路径，从该路径中提取来自受信任的内部网络的数据。 网络上的攻击者或能够影响名称解析的攻击者可以截获或修改发送到 SQL Server PDW 的数据。 这会带来篡改和信息泄露的风险。 应通过要求登录连接来缓解篡改。 为了帮助降低此风险，请在加载服务器上的**安全设置 \ 本地策略 \ 安全选项**中设置以下组策略选项： **Microsoft 网络客户端：对通信进行数字签名（始终）：已启用**  
  
-   禁用 Windows Server 2012 和更高版本上的即时文件初始化。 这是性能和安全性之间的权衡，如 "性能" 一节中所述。 您需要根据您的安全要求决定哪种最佳选择。  
  
## <a name="see-also"></a>另请参阅  
[备份和还原概述](backup-and-restore-overview.md)  
  
