---
title: 防病毒软件
description: 如果你的数据中心需要防病毒软件，请使用以下准则在分析平台系统（AP）上安装防病毒软件。 除非您的数据中心要求，否则我们建议不要安装防病毒软件。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c3687b839e52e64350591402c3aa19e9c2c54ac7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401475"
---
# <a name="antivirus-software-for-analytics-platform-system-aps"></a>用于分析平台系统（AP）的防病毒软件
如果你的数据中心需要防病毒软件，请使用以下准则在分析平台系统上安装防病毒软件。 除非您的数据中心要求，否则我们建议不要安装防病毒软件。  
  
> [!WARNING]  
> 我们强烈建议你分别为每台计算机和分析平台系统单独评估安全风险，并选择适用于每台计算机的安全风险级别的工具。 此外，我们建议在推出任何病毒保护项目之前，在完全负载下测试整个系统，以衡量稳定性和性能方面的变化。  
>   
> 病毒防护软件需要执行一些系统资源。 你必须在安装防病毒软件之前和之后执行测试，以确定对分析平台系统是否有任何性能影响。  
  
本主题基于[如何选择要在运行 SQL Server 的计算机上运行的防病毒软件](https://support.microsoft.com/kb/309422)和[知识库文章 961804](https://support.microsoft.com/kb/961804/en-us)中的指南。  
  
## <a name="exclusion-list-for-physical-hosts"></a>物理主机的排除列表  
若要在物理主机上安装防病毒软件，请排除以下目录和进程列表。 防病毒软件不应对它们进行扫描。  
  
**排除以下目录：**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-虚拟机配置目录  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual 硬盘-默认虚拟硬盘驱动器目录  
  
-   C:\clusterStorage-虚拟硬盘驱动器目录  
  
**排除这些进程：**  
  
-   虚拟机管理（Vmms）  
  
-   虚拟机工作进程（Vmwp）  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>虚拟机（Vm）的排除列表  
若要在 Vm 上安装防病毒软件，请排除以下目录和文件列表。 防病毒软件不应对它们进行扫描。  
  
**_PDW_region_-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01**和** _appliance_domain_-AD02**  
  
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
  
## <a name="see-also"></a>另请参阅  
[&#40;Analytics Platform System&#41;的设备管理任务](appliance-management-tasks.md)  
  
