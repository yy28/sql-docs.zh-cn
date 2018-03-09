---
title: "配置外部的 Windows 系统要获取远程表的副本 InfiniBand PDW"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f866890b-cad5-49ac-bbeb-848bfb26c2d5
caps.latest.revision: "11"
ms.openlocfilehash: efebff74a8c17952b39efb43006051603c624a03
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband"></a>外部 Windows 将系统配置为接收远程表副本使用 InfiniBand
描述如何购买和配置用于远程表复制功能在 SQL Server PDW 中使用无限带宽网络连接的非设备 Windows 系统。 Windows 系统将承载 SQL Server 数据库从 SQL Server PDW 数据库接收的远程表副本。 它是从设备需单独购买，并连接到设备 InfiniBand 网络。  
  
> [!NOTE]  
> 通过 InfiniBand 网络连接不需要以使用远程表副本。 如果以太网带宽满足你的需求，可以完成通过以太网网络连接。  
  
本主题介绍配置远程表复制的配置步骤之一。 有关所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>开始之前  
配置外部的 Windows 系统之前，你必须：  
  
1.  购买或提供 Windows 系统中将会收到远程副本。  
  
2.  机架控件机架中的 Windows 系统 （如果没有足够的空间） 或关闭足够到设备，以便你可以将其连接到的设备 InfiniBand 网络。  
  
3.  从设备硬件供应商购买 InfiniBand 电缆和无限带宽网络适配器。 我们建议在接收导出的数据时购买具有容错功能的两个端口的网络适配器。 两个端口的网络适配器建议，但不是一项要求。  
  
## <a name="HowToWindows"></a>外部 Windows 将系统配置为接收远程表副本  
若要配置的外部的 Windows 系统，请使用以下步骤：  
  
1.  安装到 Windows 系统的 InfiniBand 网络适配器。  
  
2.  无限带宽网络适配器连接到主 InfiniBand 开关使用 InfiniBand 电缆控件机架中。  
  
3.  安装和配置适当 Windows InfiniBand 网络适配器驱动程序。  
  
    适用于 Windows InfiniBand 驱动程序是通过 OpenFabrics 联盟，InfiniBand 供应商行业联合会开发的。  可能已使用 InfiniBand 适配器分发了正确的驱动程序。 如果没有，可以从 www.openfabrics.org 下载驱动程序。  
  
4.  在适配器上配置的每个端口的 IP 地址。 SMP 系统所需的保留地址范围中的静态 IP 地址用于此目的。 配置根据以下参数的第一个端口：  
  
    -   IP 网络地址： 172.16.132.x  
  
    -   IP 子网掩码： 255.255.128.0  
  
    -   主机的 IP 范围： 1-254  
  
    对于具有两个端口的 InfiniBand 网络适配器，配置以下参数根据第二个端口：  
  
    -   IP 网络地址： 172.16.132.x  
  
    -   IP 子网掩码： 255.255.128.0  
  
    -   主机的 IP 范围： 1-254  
  
5.  如果使用的两个端口适配器时，或多个外部的 Windows 系统连接到设备，将每个系统分配每个 IP 子网内不同的主机数。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
