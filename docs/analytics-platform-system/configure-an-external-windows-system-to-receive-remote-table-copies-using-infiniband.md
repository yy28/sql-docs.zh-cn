---
title: 将 Windows 配置为接收远程表副本
description: 介绍如何购买和配置使用 "不使用" 网络连接的非设备 Windows 系统，以便与并行数据仓库中的远程表复制功能一起使用。 Windows 系统将承载从 SQL Server PDW 数据库接收远程表复制的 SQL Server 数据库。 它与设备单独购买，并已连接到设备的 "无线网络"。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 837d41cc929d90b2494682645127f985b5768546
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401316"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>将外部 Windows 系统配置为使用 "无带宽并行" 数据仓库接收远程表副本
介绍如何购买和配置使用 "未占用网络" 连接的非设备 Windows 系统，以便与 SQL Server PDW 中的 "远程表复制" 功能配合使用。 Windows 系统将承载从 SQL Server PDW 数据库接收远程表复制的 SQL Server 数据库。 它与设备单独购买，并已连接到设备的 "无线网络"。  
  
> [!NOTE]  
> 使用远程表复制不需要通过无带宽网络进行连接。 如果以太网带宽满足你的需求，则可以通过以太网连接。  
  
本主题介绍配置远程表复制的配置步骤之一。 有关所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>开始之前  
在配置外部 Windows 系统之前，必须执行以下操作：  
  
1.  购买或提供将接收远程副本的 Windows 系统。  
  
2.  将 Windows 系统置于控制机架（如果有足够的空间）或接近于设备，以便可以将其连接到设备的无线网络。  
  
3.  从你的设备硬件供应商处购买无工作电缆和不受阻止的网络适配器。 在接收导出的数据时，我们建议购买包含两个端口的网络适配器以实现容错。 建议使用两个端口网络适配器，但这不是必需的。  
  
## <a name="HowToWindows"></a>配置外部 Windows 系统以接收远程表副本  
若要配置外部 Windows 系统，请执行以下步骤：  
  
1.  将 "无线网络适配器" 安装到 Windows 系统。  
  
2.  使用不带缆线将无线网络适配器连接到控制机架中的主要未被控制交换机。  
  
3.  为未被配置的网络适配器安装和配置适当的 Windows 驱动程序。  
  
    适用于 Windows 的不受使用的驱动程序由 OpenFabrics 联盟（一种行业协会，这是一家不受人  正确的驱动程序可能已随你的未使用适配器一起分发。 否则，可以从 www.openfabrics.org 下载该驱动程序。  
  
4.  为适配器上的每个端口配置 IP 地址。 SMP 系统需要使用为此目的而保留的地址范围中的静态 IP 地址。 根据以下参数配置第一个端口：  
  
    -   IP 网络地址： 172.16.132. x  
  
    -   IP 子网掩码：255.255.128。0  
  
    -   IP 主机范围：1-254  
  
    对于具有两个端口的无限网络适配器，请根据以下参数配置第二个端口：  
  
    -   IP 网络地址： 172.16.132. x  
  
    -   IP 子网掩码：255.255.128。0  
  
    -   IP 主机范围：1-254  
  
5.  如果使用了两个端口适配器，或多个外部 Windows 系统连接到设备，则为每个系统分配不同的主机号，每个 IP 子网。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
