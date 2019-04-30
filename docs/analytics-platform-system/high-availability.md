---
title: 分析平台系统中的高可用性 |Microsoft Docs
description: 了解 Analytics Platform System (APS) 以实现高可用性的构建方式。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5c8a562ab105e1bc40b590916d0881757036aeff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280344"
---
# <a name="analytics-platform-system-high-availability"></a>分析平台系统的高可用性
了解 Analytics Platform System (APS) 以实现高可用性的构建方式。  
  
## <a name="high-availability-architecture"></a>高可用性体系结构  
![设备体系结构](media/appliance-architecture.png "设备体系结构")  
  
## <a name="network"></a>网络  
网络可用性 APS 设备有两个 InfiniBand 网络。 如果其中一个 InfiniBand 网络出现故障，另一个是仍然可用。 此外，Active Directory 已复制域控制器以将传入的请求解析为正确的 InfiniBand 网络。  
  
有关详细信息，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。  
  
## <a name="storage"></a>存储  
为了保证数据的安全，AP 使用 RAID 1 镜像要维护的所有用户数据的两个副本。 在磁盘发生故障时，硬件系统重新生成到备用的磁盘上的数据，并设置存在磁盘故障警报。  
  
若要联机保持数据可用，APS 使用 Windows 存储空间和群集共享的卷来管理直连存储中的用户数据磁盘。 没有一个存储池，每个组织到群集共享卷的可供通过装入点的计算节点主机的数据缩放单位。  
  
若要确保存储池会保持联机状态，数据缩放单位中的每个主机具有不会不会故障转移 ISCSI 虚拟机。 此体系结构很重要，因为如果主机发生故障，该数据是通过数据缩放单位中的其他主机仍可访问。  
  
## <a name="hosts"></a>主机  
对于主机可用性的所有主机配置为 Windows 故障转移群集。 每个机架拥有被动主机。 （可选） 在第一个机架，控制 SQL Server 并行数据仓库 (PDW) 和设备 fabric，可以有第二个被动主机。 如果主机发生故障，为故障转移，配置的虚拟机将故障转移到被动的可用主机。  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 节点和设备的构造  
为 PDW 节点和设备结构的高可用性，AP 使用虚拟化。 每个虚拟机中运行的 PDW 和设备结构组件。  
  
每个虚拟机被指 Windows 故障转移群集中的角色。 当虚拟机失败时，群集重新启动它可用被动主机上。 使用 System Center Virtual Machine Manager 部署虚拟机。 故障转移时，被动主机上运行的虚拟机是仍然能够通过 InfiniBand 网络访问其用户数据。  
  
控制节点和计算节点虚拟机分别配置为单节点群集。 单节点群集为群集资源，以确保群集始终使用的活动的 InfiniBand IP 管理 InfiniBand 网络。 单节点群集管理虚拟机中运行的 PDW 进程。 例如，单节点群集具有 SQL Server 和数据移动服务 (DMS) 作为资源，以便它可以按正确的顺序启动它们。 控制节点 VM 还可以控制其他业务流程主机运行的 Vm 的启动顺序。  
  
