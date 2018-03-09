---
title: "分析平台系统的高可用性"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "介绍如何分析平台系统 (AP) 以实现高可用性而设计。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 5ab245e9-0316-4d25-a626-4745ce856925
caps.latest.revision: "9"
ms.openlocfilehash: 11733b45ba25f625ea2d3d601939973e9137b15d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="analytics-platform-system-high-availability"></a>分析平台系统的高可用性
介绍如何分析平台系统 (AP) 以实现高可用性而设计。  
  
## <a name="high-availability-architecture"></a>高可用性体系结构  
![设备体系结构](media/appliance-architecture.png "设备体系结构")  
  
## <a name="network"></a>网络  
对于网络可用性 AP 设备具有两个 InfiniBand 网络。 如果其中一个 InfiniBand 网络出现故障，另一个控制器是仍然可用。 此外，Active Directory 已复制域控制器为传入的请求解析到正确的 InfiniBand 网络。  
  
有关详细信息，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。  
  
## <a name="storage"></a>存储器  
为了保护数据的安全，AP，请使用 RAID 1 镜像来维护的所有用户数据的两个副本。 在发生磁盘故障，硬件系统将重新生成到备用的磁盘上的数据，并设置存在磁盘故障警报。  
  
若要联机保持数据可用，AP 使用 Windows 存储空间和群集共享的卷来管理直连的存储中的用户数据磁盘。 没有一个存储池，每个组织到群集共享卷哪些可供通过装入点的计算节点主机使用的数据缩放单位。  
  
若要确保存储池会保持联机状态，在数据缩放单位中的每个主机具有不故障转移 ISCSI 虚拟机。 此体系结构很重要，因为如果主机发生故障的数据是通过数据缩放单位中的其他主机仍可访问。  
  
## <a name="hosts"></a>主机  
对于主机可用性的所有主机配置为 Windows 故障转移群集中。 每个机架拥有被动主机。 （可选） 的第一个机架，控制 SQL Server 并行数据仓库 (PDW) 和设备构造，可以有第二个被动主机。 如果主机发生故障，为故障转移，配置的虚拟机将故障转移到被动主机上可用。  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 节点和装置结构  
对于 PDW 节点和装置结构的高可用性，AP 使用虚拟化。 每个 PDW 和装置 fabric 组件在虚拟机上运行。  
  
每个虚拟机被指 Windows 故障转移群集中的角色。 当虚拟机失败时，群集重新启动该可用性的被动主机上。 使用 System Center Virtual Machine Manager 部署的虚拟机。 故障转移发生后，在被动的主机上运行的虚拟机是仍可以通过 InfiniBand 网络访问其用户数据。  
  
控制节点和计算节点虚拟机分别配置为单节点群集。 单节点群集为群集资源以确保群集始终使用 active InfiniBand IP 管理 InfiniBand 网络。 单节点群集管理虚拟机中运行的 PDW 进程。 例如，单节点群集具有 SQL Server 和数据移动服务 (DMS) 作为资源，以便它可以按正确的顺序启动它们。 控制节点 VM 还控制在业务流程主机运行的其他 Vm 的启动顺序。  
  
