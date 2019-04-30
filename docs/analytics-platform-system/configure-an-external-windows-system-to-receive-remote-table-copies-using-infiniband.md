---
title: 配置 Windows 以接收远程表副本的并行数据仓库 |Microsoft Docs
description: 介绍如何购买和配置用于远程表复制功能在并行数据仓库中使用 InfiniBand 网络连接的非设备 Windows 系统。 Windows 系统将承载 SQL Server 数据库从 SQL Server PDW 数据库接收远程表副本。 它是独立于设备购买并连接到设备 InfiniBand 网络。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ed7122f497b0bdebd893eec75606bbb6382e9a73
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224863"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>配置外部 Windows 系统以接收远程表副本使用 InfiniBand 的并行数据仓库
介绍如何购买和配置用于远程表复制功能在 SQL Server PDW 中使用 InfiniBand 网络连接的非设备 Windows 系统。 Windows 系统将承载 SQL Server 数据库从 SQL Server PDW 数据库接收远程表副本。 它是独立于设备购买并连接到设备 InfiniBand 网络。  
  
> [!NOTE]  
> 通过 InfiniBand 网络连接不需要使用远程表副本。 如果以太网带宽满足你的需求，可以完成通过以太网网络进行连接。  
  
本主题介绍配置远程表复制的配置步骤之一。 所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>开始之前  
配置外部 Windows 系统之前，你必须：  
  
1.  购买或提供一个 Windows 系统，将收到远程副本。  
  
2.  机架控件机架中的 Windows 系统 （如果没有足够的空间） 或关闭足够到设备，以便可以将其连接到设备 InfiniBand 网络。  
  
3.  从你的设备硬件供应商购买 InfiniBand 电缆和 InfiniBand 网络适配器。 我们建议购买具有容错能力的两个端口的网络适配器，接收导出的数据时。 两个端口网络适配器建议，但不是一项要求。  
  
## <a name="HowToWindows"></a>配置外部 Windows 系统以接收远程表副本  
若要配置外部 Windows 系统，请使用以下步骤：  
  
1.  InfiniBand 网络适配器安装到您的 Windows 系统。  
  
2.  InfiniBand 网络适配器连接到主 InfiniBand 开关使用 InfiniBand 电缆在控件机架中。  
  
3.  安装和配置 InfiniBand 网络适配器的相应 Windows 驱动程序。  
  
    Windows 的 InfiniBand 驱动程序开发的 OpenFabrics 联盟的 InfiniBand 供应商。  使用 InfiniBand 适配器中，可能已分发的正确驱动程序。 如果没有，可以从 www.openfabrics.org 下载驱动程序。  
  
4.  在适配器上配置的每个端口的 IP 地址。 SMP 系统需要通过一系列保留的地址的静态 IP 地址用于此目的。 配置根据以下参数的第一个端口：  
  
    -   IP 网络地址：172.16.132.x  
  
    -   IP 子网掩码：255.255.128.0  
  
    -   主机的 IP 范围：1-254  
  
    对于具有两个端口的 InfiniBand 网络适配器，配置以下参数根据第二个端口：  
  
    -   IP 网络地址：172.16.132.x  
  
    -   IP 子网掩码：255.255.128.0  
  
    -   主机的 IP 范围：1-254  
  
5.  如果使用两个端口适配器，或多个外部 Windows 系统的连接到设备，将每个系统分配每个 IP 子网内不同的主机数。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
