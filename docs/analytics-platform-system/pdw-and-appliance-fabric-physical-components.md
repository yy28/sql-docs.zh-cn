---
title: 设备物理组件的分析平台系统 |Microsoft Docs
description: 名称和说明 PDW 和设备结构物理组件。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0adbd92d1a29a98a80de65268c53ea63e3941d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639939"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>设备物理组件的分析平台系统
名称和说明 PDW 和设备结构物理组件。 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>组件图  
这将显示的物理组件和计算 6 节点设备在第一个机架中的位置的名称。  
  
![PDW 区域组件名称-HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
PDW 组件的实际名称是 PDW 区域名称后, 跟一个破折号，然后是组件名称。 例如，如果 PDW 区域名称，PDW123 的实际名称是**PDW123 CTL01**， **PDW123-CMP01**，等等。  
  
同样，设备 fabric 组件的实际名称是设备域，跟一个破折号，然后是组件名称。 例如，如果 FSW123 设备域，则设备 fabric Vm 均**FSW123 WDS**， **FSW123 AD01**， **FSW123 VMM**，等等。  
  
下面是包含 6 个计算节点的 PDW 区域的合并的视图。  
  
![PDW 组件名称](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW 组件  
PDW 虚拟机是 PDW 区域的一部分。  
  
*PDW_region*-CTL01  
运行管理节点的虚拟机。 此运行上 HST01，可以故障转移到 HST02。  
  
> [!WARNING]  
> SQL Server PDW 不支持通过使用 Hyper-v 管理器创建 CTL01 虚拟机的快照。 快照依赖于本地存储，如果虚拟机尝试故障转移到其备份，则会导致出现错误。 创建快照也会导致可靠性问题其他虚拟机的故障转移到被动服务器。  
  
*PDW_region*-通过 CMP01 *PDW_Region*-CMP06  
运行计算节点的虚拟机。 在此 6 计算节点关系图中，通过 HSA06 运行的主机 HSA01 分别计算节点 Vm CMP01 CMP06 通过。  
  
## <a name="fabric"></a>设备 Fabric 组件  
这些组件是设备结构的一部分。  
  
### <a name="virtual-machines"></a>虚拟机  
*appliance_domain*-WDS  
此虚拟机承载 Windows 部署服务 (WDS)，它分析平台系统使用通过设备网络部署 Windows 操作系统。 它还托管 DHCP 服务，它允许设备主机以加入设备网络而无需预先配置的 IP 地址。  
  
*Appliance_domain*-WDS 虚拟机上 HST01 运行并且可以故障转移到 HST02。 WDS 虚拟机和 VMM 虚拟机，部署在物理主机上 Windows 设备安装过程。 在设备生命周期中，WDS 和 VMM 执行替换主机等操作。  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM) 的虚拟机中运行，并可以故障转移到 HST02。 VMM 托管 System Center 部署物理主机上的操作系统。 VMM 还提供了 Windows Server Update Services (WSUS) 以应用或删除在所有主机和虚拟机上的 Windows 更新。  
  
*appliance_domain*-AD01， *appliance_domain*-AD02  
Active Directory 域服务，包含域名系统 (DNS)，在 HST01 和 HST02 上运行的虚拟机中。 有关设备的高可用性，AD01 和 AD02 是复制的域控制器和它们执行操作不会故障转移。 如果一个失败，另一个是已提供正确的数据。  
  
*appliance_domain*-ISCSI01  
附加存储 (HSA01 HSA06) 在每台主机上运行一台 ISCSI 虚拟机。 此 VM 执行不会故障转移。  
  
### <a name="hosts"></a>主机  
*appliance_domain*-通过 HST01 *appliance_domain*-HST06  
为 PDW 控制节点和设备 fabric 虚拟机主机。 HST03 是可选的被动主机。  
  
*appliance_domain*-通过 HSA01 *appliance_domain*-HSA08  
具有附加存储 (HSA) 的主机。 每个 HAS 主机运行一个计算节点 VM，另一个 ISCSI VM。  
  
### <a name="cluster-for-pdw"></a>PDW 的群集  
*appliance_domain*-WFOHST01  
PDW 群集名为 WFOHST01。 它管理的所有物理主机和虚拟机属于 PDW。  
  
### <a name="direct-attached-storage"></a>直接附加的存储  
*appliance_domain*-通过 DAS01 *appliance_domain*-DAS03  
这是连接到计算节点的直接附加的存储。 HP 具有一个 DAS 为每个两个计算节点。 Dell 和量程使用为每隔三个计算节点的一个直连存储。  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[设备配置&#40;分析平台系统&#41;](appliance-configuration.md)  
[设备管理任务&#40;分析平台系统&#41;](appliance-management-tasks.md)  
  
