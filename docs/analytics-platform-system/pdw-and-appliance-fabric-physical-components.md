---
title: 设备物理组件的分析平台系统 |Microsoft 文档
description: 名称和 PDW 和装置 fabric 物理组件的说明。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0adbd92d1a29a98a80de65268c53ea63e3941d07
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="appliance-physical-components---analytics-platform-system"></a>设备物理组件的分析平台系统
名称和 PDW 和装置 fabric 物理组件的说明。 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>组件图  
这将显示为名称的物理组件和它们位于在第一个 6 计算节点设备的机架中。  
  
![PDW 区域组件名称-HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
PDW 组件的实际名称是 PDW 区域名称后, 跟一个破折号，后面加上组件名称。 例如，如果 PDW 区域名称，PDW123 的实际名称是**PDW123 CTL01**， **PDW123 CMP01**等。  
  
同样，设备 fabric 组件的实际名称是设备域后, 跟一个破折号，后面加上组件名称。 例如，如果 FSW123 设备域，则设备 fabric Vm 是**FSW123 WDS**， **FSW123 AD01**， **FSW123 VMM**等。  
  
下面是具有 6 计算节点的 PDW 区域的合并的视图。  
  
![PDW 组件名称](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW 组件  
PDW 虚拟机将 PDW 区域的一部分。  
  
*PDW_region*-CTL01  
虚拟机中运行的控件节点。 这在 HST01 上运行，并可以故障转移到 HST02。  
  
> [!WARNING]  
> SQL Server PDW 不支持通过使用 Hyper-v 管理器中创建 CTL01 虚拟机的快照。 快照依赖于本地存储区，这将导致错误，如果虚拟机尝试故障转移到其备份。 创建快照也会导致可靠性问题与其他 VM 的该故障转移到被动的服务器。  
  
*PDW_region*-通过 CMP01 *PDW_Region*-CMP06  
运行计算节点的虚拟机。 在此 6 计算节点图中，通过运行 HSA06 主机 HSA01 分别计算节点 Vm CMP01 CMP06 通过。  
  
## <a name="fabric"></a>设备 Fabric 组件  
这些组件是设备结构的一部分。  
  
### <a name="virtual-machines"></a>虚拟机  
*appliance_domain*-WDS  
此虚拟机承载 Windows 部署服务 (WDS)，分析平台系统用通过设备网络部署 Windows 操作系统。 它还承载让设备主机，而无需预先配置的 IP 地址加入设备网络的 DHCP 服务。  
  
*Appliance_domain*-WDS 虚拟机在 HST01 上运行，并且可以故障转移到 HST02。 WDS 虚拟机和 VMM 虚拟机，部署在物理主机上 Windows 设备安装的过程。 在设备生命周期，WDS 和 VMM 执行操作，如替换主机。  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM) 在虚拟机中运行，并可以故障转移到 HST02。 VMM 托管系统中心来部署物理主机上的操作系统。 VMM 还提供了 Windows Server Update Services (WSUS) 应用或删除的所有主机和虚拟机的 Windows 更新。  
  
*appliance_domain*-AD01， *appliance_domain*-AD02  
HST01 和 HST02 情况下，active Directory 域服务，其中包含域名系统 (DNS)，在虚拟机中运行。 获得的设备的高可用性，AD01 和 AD02 是复制的域控制器，并且它们不是故障转移。 如果其中一个失败，另一个时已使用正确的数据。  
  
*appliance_domain*-ISCSI01  
连接存储 (HSA01 HSA06) 在每个主机上运行一个 ISCSI 虚拟机。 此 VM 执行不的故障转移。  
  
### <a name="hosts"></a>主机  
*appliance_domain*-通过 HST01 *appliance_domain*-HST06  
为 PDW 控制节点和装置 fabric 虚拟机主机。 HST03 是可选的被动主机。  
  
*appliance_domain*-通过 HSA01 *appliance_domain*-HSA08  
使用连接存储 (HSA) 主机。 每个 HAS 主机运行一个计算节点 VM，另一个 ISCSI VM。  
  
### <a name="cluster-for-pdw"></a>PDW 的群集  
*appliance_domain*-WFOHST01  
PDW 群集名为 WFOHST01。 它管理的所有物理主机和虚拟机属于 PDW。  
  
### <a name="direct-attached-storage"></a>直连的存储  
*appliance_domain*-通过 DAS01 *appliance_domain*-DAS03  
这是连接到计算节点的直接附加的存储。 HP 具有一个 DAS 为每个两个计算节点。 Dell 和量程使用为每隔三个计算节点的一个直连存储。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[设备配置&#40;分析平台系统&#41;](appliance-configuration.md)  
[设备管理任务&#40;分析平台系统&#41;](appliance-management-tasks.md)  
  
