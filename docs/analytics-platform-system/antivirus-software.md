---
title: 防病毒软件-分析平台系统 |Microsoft 文档
description: 如果你的数据中心要求防病毒软件，使用这些准则在分析平台系统上安装防病毒软件。 我们建议不安装防病毒软件，除非它是你的数据中心的硬性要求。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5d9ff6848d2df43408613d41dc7a0e6f8c1b0b8c
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550039"
---
# <a name="antivirus-software-for-analytics-platform-system"></a>分析平台系统的防病毒软件
如果你的数据中心要求防病毒软件，使用这些准则在分析平台系统上安装防病毒软件。 我们建议不安装防病毒软件，除非它是你的数据中心的硬性要求。  
  
> [!WARNING]  
> 我们强烈建议您单独评估安全风险的每台计算机和分析平台系统作为一个整体，并且你选择的工具，适用于每台计算机的安全风险级别。 此外，我们建议在推送任何防病毒项目之前，测试整个系统负载很完整在稳定性和性能测量的任何更改。  
>   
> 病毒保护软件需要执行某些系统资源。 你必须执行测试之前和之后安装防病毒软件以确定是否存在任何对分析平台系统上的性能影响。  
  
本主题基于中的指导[如何选择要在运行 SQL Server 的计算机上运行的防病毒软件](http://support.microsoft.com/kb/309422)和[KB 文章 961804](http://support.microsoft.com/kb/961804/en-us)。  
  
## <a name="exclusion-list-for-physical-hosts"></a>物理主机的排除列表  
若要在物理主机上安装防病毒软件，排除以下目录和进程的列表。 这些不应通过防病毒软件扫描。  
  
**排除这些目录：**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-虚拟机配置目录  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual 硬盘的默认虚拟硬盘驱动器目录  
  
-   C:\clusterStorage-虚拟硬盘驱动器目录  
  
**排除这些进程：**  
  
-   虚拟机管理 (Vmms.exe)  
  
-   虚拟机工作进程 (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>虚拟机 (Vm) 的排除列表  
若要在虚拟机上安装防病毒软件，排除以下目录和文件的列表。 这些不应通过防病毒软件扫描。  
  
***PDW_region*-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain *-AD01**和 ***appliance_domain *-AD02**  
  
-   无限制  
  
**计算节点 Vm**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain*-VMM**  
  
-   无限制  
  
***appliance_domain*-WDS**  
  
-   无限制  
  
***appliance_domain*-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>另请参阅  
[设备管理任务&#40;分析平台系统&#41;](appliance-management-tasks.md)  
  
