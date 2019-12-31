---
title: 打开或关闭设备
description: 为分析平台系统开启或关闭设备
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee70338b5a46ec60d808e489d982fd80692c5d1d
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400619"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>为分析平台系统开启或关闭设备
本主题介绍如何在运行并行数据仓库的分析平台 Systemappliance 上通电或关闭。 移动分析平台系统设备时，或在发生灾难性故障后，使用本主题来打开设备。  
  
打开和关闭设备与启动和停止设备服务不同。 有关此主题的信息，请参阅[PDW 服务状态 &#40;分析平台系统&#41;](pdw-services-status.md)。 有关打开或关闭 SQL Server 2008 并行数据仓库的信息，请参阅 SQL Server 2008 并行数据仓库帮助文件。 有关打开或关闭 SQL Server 2012 AU1 或 AU2 并行数据仓库的信息，请参阅这些版本的帮助文件。  
  
当这些说明指定连接到 SQL Server PDW 节点时，连接可以使用连接的设备（KVM）或使用远程桌面进行远程连接。 某些操作必须是物理的（打开电源开关），一些操作可以是物理的，也可以是使用 Windows 命令。  
  
可以使用分配给节点的 IP 地址，或通过使用**故障转移群集管理器**（**Cluadmin.msc**）或**hyper-v 管理器**（**virtmgmt**）应用程序的**HST01**计算机连接到 SQL Server PDW 节点，并右键单击节点名称。  
  
## <a name="PowerOff"></a>关闭设备电源  
  
### <a name="before-you-begin"></a>开始之前  
在关闭设备之前，应结束设备上的所有活动。 结束所有活动：  
  
-   使用管理控制台的 "**会话**" 页可以识别当前用户。 与他们联系并要求他们注销。  
  
-   如有必要，您可以使用**KILL**语句来强制终止客户端连接。 在终止连接时请小心。 在中断时，某些事务处理过程（如长时间运行的更新）必须回滚活动，SQL Server 才能完成数据库的恢复。 回滚部分完成的更新或删除可能非常耗时。  
  
### <a name="to-power-off-the-appliance"></a>关闭设备电源  
  
> [!WARNING]  
> 必须按列出的准确顺序执行所有步骤，并且必须在执行下一步之前完成每个步骤（除非另有说明）。 不按顺序执行步骤或在不等待每个步骤完成的情况下，可能会导致设备在以后通电时出现错误。  
  
1.  连接到 PDW 控制节点（**_PDW_region_CTL01** ）并登录到 Analytics Platform System 设备域管理员帐户。  
  
2.  运行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`打开**Configuration Manager**。  
  
3.  在 Configuration Manager 的 "**并行数据仓库拓扑**" 菜单下，单击 "**服务状态**" 选项卡，然后单击 "**停止区域**" 停止 PDW 服务。   
  
4.  连接到** _appliance_domain_-HST01**并登录到设备域管理员帐户。  
  
5.  使用**故障转移群集管理器**连接到** _appliance_domain_WFOHST01**群集，如果未自动连接，则在导航窗格中单击 "**角色**"。 在 "**角色**" 窗格中：  
  
    1.  多选所有虚拟机。 右键单击它们，然后选择 "**关闭**"。  
  
    2.  等待所有选定的 Vm 关闭。  
  
6.  关闭**故障转移群集管理器**应用程序。  
  
7. 关闭所有服务器（ ** _appliance_domain_-HST01 除外）**。  
  
8. 关闭** _appliance_domain_HST01**服务器。  
  
9. 关闭配电装置（Pdu）。  
  
## <a name="PowerOn"></a>开启设备  
  
### <a name="to-power-on-the-appliance"></a>启用设备电源  
  
> [!WARNING]  
> 必须按列出的准确顺序执行所有步骤，并且必须在执行下一步之前完成每个步骤（除非另有说明）。 不按顺序执行或不等待每个步骤完成的步骤会导致启动错误。  
  
1.  接通电源分配单元（PDU），并等待交换机自动启动。  
  
2.  打开** _appliance_domain_-HST01**服务器。  
  
3.  以设备域管理员身份登录到** _appliance_domain_-HST01** 。  
  
4.  启动**Hyper-v 管理器**程序（**virtmgmt**）并连接到** _appliance_domain_-HST01** （如果默认情况下未连接）。  
  
    1.  如果无法通过名称进行连接，因为** _PDW_region_-AD01**未运行，请尝试使用 IP 地址进行连接。  
  
    2.  在 "**虚拟机**" 窗格中，找到** _PDW_region_-AD01** ，并确认其正在运行。 如果没有，请启动此 VM，并等待其完全启动。  
  
5.  打开设备中的其余服务器。  
  
6.  在**HST01**上，从**hyper-v 管理器**以设备域管理员身份登录：  
  
    1.  连接到** _appliance_domain_-HST02**。  
  
    2.  在 "**虚拟机**" 窗格中，找到** _PDW_region_-AD02**并确认该程序正在运行。  如果没有，请启动此 VM，并等待其完全启动。  
  
7.  使用**故障转移群集管理器**连接到** _appliance_domain_WFOHST01**群集，如果未自动连接，则在**导航**窗格中单击 "**角色**"。 在 "**角色**" 窗格中：  
  
    1.  选择 "多个"，右键单击所有虚拟机，然后单击 "**启动**"。  
  
    2.  等待所有选定的 Vm 在继续下一步之前完成启动。  
  
    3.  如果 Vm 发生了故障转移，请将其关闭，然后移动它们，然后在正确的主主机上重新启动它们。  
  
8. 如果需要，请从**HST01**断开连接。  
  
9. 使用设备的域管理员帐户连接到** _PDW_region_-CTL01** 。  
  
10. 运行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`启动**Configuration Manager**。  
  
11. 在**Configuration Manager**的 "**并行数据仓库拓扑**" 菜单中，单击 "**服务状态**" 选项卡，然后单击 "**开始区域**" 以启动 PDW 服务。  
  
### <a name="to-verify-the-appliance-health"></a>验证设备运行状况  
设备启动后，打开**管理控制台**，并检查运行状况页面中是否有可能指出失败情况的警报。 有关详细信息，请参阅[使用管理控制台监视设备 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。  
  
## <a name="see-also"></a>另请参阅  
[&#40;Analytics Platform System&#41;的设备管理任务](appliance-management-tasks.md)  
  
