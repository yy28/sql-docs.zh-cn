---
title: 防病毒软件的分析平台系统 |Microsoft Docs
description: 如果你的数据中心需要防病毒软件，使用这些准则在分析平台系统上安装防病毒软件。 我们建议不要安装防病毒软件，除非它是数据中心的硬性要求。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c5b9a1eddf8bf06a9d9e5b59754b2c6a34b94267
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524471"
---
# <a name="antivirus-software-for-analytics-platform-system"></a>Analytics Platform system 防病毒软件
如果你的数据中心需要防病毒软件，使用这些准则在分析平台系统上安装防病毒软件。 我们建议不要安装防病毒软件，除非它是数据中心的硬性要求。  
  
> [!WARNING]  
> 我们强烈建议您单独评估每台计算机和分析平台系统的整体安全风险并且您选择的工具，适用于每台计算机的安全风险级别。 此外，我们建议您推出任何病毒防护项目之前，测试整个系统进行完整负载中的稳定性和性能的度量值的任何更改。  
>   
> 病毒保护软件需要执行一些系统资源。 您必须执行测试之前和之后安装防病毒软件以确定是否在分析平台系统上的任何性能影响。  
  
本主题基于中的指导[如何选择要在运行 SQL Server 的计算机上运行的防病毒软件](https://support.microsoft.com/kb/309422)并[KB 文章 961804](https://support.microsoft.com/kb/961804/en-us)。  
  
## <a name="exclusion-list-for-physical-hosts"></a>物理主机的排除列表  
若要在物理主机上安装防病毒软件，排除以下目录和进程的列表。 这些不应通过防病毒软件扫描。  
  
**排除这些目录：**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-虚拟机配置目录  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual 硬盘的默认虚拟硬盘驱动器目录  
  
-   C:\clusterStorage-虚拟硬盘驱动器上的目录  
  
**排除这些进程：**  
  
-   虚拟机管理 (Vmms.exe)  
  
-   虚拟机工作进程 (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>虚拟机 (Vm) 的排除列表  
若要在 Vm 上安装防病毒软件，排除以下目录和文件的列表。 这些不应通过防病毒软件扫描。  
  
**_PDW_region_-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01**并 **_appliance_domain_-AD02**  
  
-   无限制  
  
**计算节点 Vm**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-VMM**  
  
-   无限制  
  
**_appliance_domain_-WDS**  
  
-   无限制  
  
**_appliance_domain_-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>请参阅  
[设备管理任务&#40;分析平台系统&#41;](appliance-management-tasks.md)  
  
