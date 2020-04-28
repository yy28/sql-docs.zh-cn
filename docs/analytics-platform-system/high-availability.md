---
title: 高可用性
description: 了解如何设计分析平台系统（AP）以实现高可用性。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6246ed25909a2e366d8bbafcd912a4fd923cc84a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401105"
---
# <a name="analytics-platform-system-high-availability"></a>分析平台系统高可用性
了解如何设计分析平台系统（AP）以实现高可用性。  
  
## <a name="high-availability-architecture"></a>高可用性体系结构  
![设备体系结构](media/appliance-architecture.png "设备体系结构")  
  
## <a name="network"></a>网络  
对于网络可用性，AP 设备具有两个未经过网络。 如果某个未通过网络出现故障，另一个网络仍可用。 此外，Active Directory 已将域控制器复制到正确的域控制器，以将传入的请求解析为正确的可处理网络  
  
有关详细信息，请参阅[配置无线网络适配器](configure-infiniband-network-adapters.md)。  
  
## <a name="storage"></a>存储  
为了保证数据的安全，AP 使用 RAID 1 镜像来维护所有用户数据的两个副本。 磁盘发生故障时，硬件系统会将数据重建到备用磁盘上，并设置出现磁盘故障的警报。  
  
为了使数据保持在线状态，AP 使用 Windows 存储空间和群集共享卷来管理直连存储中的用户数据磁盘。 对于群集共享卷，每个数据扩展单元有一个存储池，这些存储池可通过装入点向计算节点主机提供。  
  
为了确保存储池保持联机状态，数据缩放单位中的每个主机都有一个不会进行故障转移的 ISCSI 虚拟机。 此体系结构很重要，因为如果主机发生故障，则仍可通过数据缩放单位中的其他主机访问数据。  
  
## <a name="hosts"></a>主机  
对于主机可用性，所有主机都配置为 Windows 故障转移群集。 每个机架都有被动主机。 （可选）第一个机架（控制 SQL Server 并行数据仓库（PDW）和设备构造）可以有第二个被动主机。 如果主机发生故障，则为故障转移配置的虚拟机将故障转移到可用的被动主机。  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 节点和设备结构  
为了实现 PDW 节点和设备 fabric 的高可用性，AP 使用虚拟化。 每个 PDW 和设备结构组件都在虚拟机中运行。  
  
每个虚拟机都定义为 Windows 故障转移群集中的角色。 当虚拟机发生故障时，群集会在可用的被动主机上重新启动它。 使用 System Center Virtual Machine Manager 部署虚拟机。 发生故障转移时，被动主机上运行的虚拟机仍可以通过未使用的网络访问其用户数据。  
  
控制节点和计算节点虚拟机每个虚拟机都配置为单节点群集。 单节点群集将非群集网络作为群集资源进行管理，以确保群集始终使用活动的可管理的 IP。 单节点群集管理在虚拟机中运行的 PDW 进程。 例如，单节点群集将 SQL Server 和数据移动服务（DMS）作为资源，以便可以按正确的顺序启动它们。 控制节点 VM 还控制在业务流程主机上运行的其他 Vm 的启动顺序。  
  
