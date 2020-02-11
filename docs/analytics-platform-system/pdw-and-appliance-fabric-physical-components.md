---
title: 设备物理组件
description: PDW 和设备结构物理组件的名称和描述。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5cbed66f53189668518e04848002ae69adb8c614
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400921"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>设备物理组件-分析平台系统
PDW 和设备结构物理组件的名称和描述。 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>组件图  
这会显示物理组件的名称，以及它们位于6计算节点设备的第一个机架中的位置。  
  
![PDW 区域组件名称 - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
PDW 组件的实际名称是 PDW 区域名称，后跟一个破折号，再后跟组件名称。 例如，如果 PDW 区域名称为 PDW123，则实际名称为**PDW123-CTL01**、 **PDW123-pqth4a-cmp01**等。  
  
同样，设备结构组件的实际名称是设备域，后跟一个破折号，再后跟组件名称。 例如，如果设备域为 FSW123，则设备结构 Vm 为**FSW123**、 **FSW123-AD01**、 **FSW123**，等等。  
  
下面是包含6个计算节点的 PDW 区域的合并视图。  
  
![PDW 组件名称](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW 组件  
PDW 虚拟机是 PDW 区域的一部分。  
  
*PDW_region*-CTL01  
运行控制节点的虚拟机。 这会在 HST01 上运行，并可故障转移到 HST02。  
  
> [!WARNING]  
> SQL Server PDW 不支持使用 Hyper-v 管理器创建 CTL01 虚拟机的快照。 快照依赖于本地存储，如果虚拟机尝试故障转移到其备份，这将导致错误。 创建快照还会导致故障转移到被动服务器的其他 VM 的可靠性问题。  
  
通过*PDW_Region* *PDW_region*-pqth4a-cmp01-CMP06  
运行计算节点的虚拟机。 在此6计算节点图中，主机 HSA01 到 HSA06 分别运行计算节点 Vm PQTH4A-CMP01 到 CMP06。  
  
## <a name="fabric"></a>设备结构组件  
这些组件是设备结构的一部分。  
  
### <a name="virtual-machines"></a>虚拟机  
*appliance_domain*-WDS  
此虚拟机托管 Windows 部署服务（WDS），分析平台系统使用通过设备网络部署 Windows 操作系统。 它还托管 DHCP 服务，这允许设备主机无需预配置的 IP 地址即可加入设备网络。  
  
*Appliance_domain*WDS 虚拟机在 HST01 上运行，并可故障转移到 HST02。 WDS 虚拟机和 VMM 虚拟机在设备安装过程中在物理主机上部署 Windows。 在设备生命周期内，WDS 和 VMM 会执行一些操作，例如替换主机。  
  
*appliance_domain*-VMM  
Virtual Machine Manager （VMM）在虚拟机中运行，并且可以故障转移到 HST02。 VMM 托管 System Center，以将操作系统部署到物理主机上。 VMM 还提供 Windows Server Update Services （WSUS）以在所有主机和虚拟机中应用或删除 Windows 更新。  
  
*appliance_domain*-AD01， *appliance_domain*-AD02  
Active Directory 域服务（其中包含域名系统（DNS））将在 HST01 和 HST02 上的虚拟机中运行。 为了实现设备的高可用性，AD01 和 AD02 会被复制到域控制器，并且不会进行故障转移。 如果一个失败，则已有一个正确的数据可用。  
  
*appliance_domain*-ISCSI01  
一个 ISCSI 虚拟机在附加了存储的每个主机（HSA01-HSA06）上运行。 此 VM 不会进行故障转移。  
  
### <a name="hosts"></a>主机  
通过*appliance_domain* *appliance_domain*-HST01-HST06  
PDW 控制节点和设备结构虚拟机的主机。 HST03 是一个可选的被动主机。  
  
通过*appliance_domain* *appliance_domain*-HSA01-HSA08  
已附加存储的主机（HSA）。 每个主机都有一个计算节点 VM 和一个 ISCSI VM。  
  
### <a name="cluster-for-pdw"></a>PDW 的群集  
*appliance_domain*-WFOHST01  
PDW 群集名为 WFOHST01。 它管理属于 PDW 的所有物理主机和虚拟机。  
  
### <a name="direct-attached-storage"></a>直接连接的存储  
通过*appliance_domain* *appliance_domain*-DAS01-DAS03  
这是连接到计算节点的直接连接存储。 HP 为每两个计算节点提供一个 DAS。 对于每三个计算节点，Dell 和量程有一个 DAS。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[设备配置 &#40;分析平台系统&#41;](appliance-configuration.md)  
[&#40;Analytics Platform System&#41;的设备管理任务](appliance-management-tasks.md)  
  
