---
title: 电源设备打开或关闭的分析平台系统 |Microsoft Docs
description: 用于分析平台系统的电源打开或关闭的设备
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a8be7ec364a257752576fa150434a67a92c28d9c
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909507"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>用于分析平台系统的电源打开或关闭的设备
本主题介绍如何打开或关闭在分析平台 Systemappliance 电源电源运行的并行数据仓库。 使用本主题分析平台系统 appliance 移动时，或电源在一台设备上发生灾难性的电源发生故障后。  
  
打开和关闭增强设备不是与启动和停止设备服务相同。 有关该主题的信息，请参阅[PDW 服务状态&#40;Analytics Platform System&#41;](pdw-services-status.md)。 打开或关闭 SQL Server 2008 并行数据仓库方面的信息，请参阅 SQL Server 2008 并行数据仓库的帮助文件。 打开或关闭 SQL Server 2012 AU1 或 AU2 并行数据仓库方面的信息，请参阅这些版本的帮助文件。  
  
当这些说明指定连接到 SQL Server PDW 节点时，连接可以本地使用附加的设备 (KVM) 或远程使用远程桌面。 （打开电源开关） 的物理计算机和一些模块 （如关闭），必须为某些操作可以是物理计算机或通过使用 Windows 的命令。  
  
可以使用分配给节点，或从分配的 IP 地址建立到 SQL Server PDW 节点的连接**HST01**通过使用计算机**故障转移群集管理器**(**cluadmin.msc**)或**Hyper-v 管理器**(**virtmgmt.msc**) 应用程序，然后右键单击节点名称。  
  
## <a name="PowerOff"></a>关闭设备电源  
  
### <a name="before-you-begin"></a>开始之前  
关闭设备电源之前, 应最终在设备上的所有活动。 若要结束的所有活动：  
  
-   使用**会话**的管理控制台来标识当前用户的页面。 与他们联系并要求他们注销。  
  
-   如有必要，可以使用**KILL**语句，以强制客户端连接终止。 终止时要格外小心连接。 时中断，某些事务的进程，如长时间运行的更新，必须在 SQL Server 之前回滚活动可以完成恢复数据库。 部分已完成的更新或删除正在回滚，会耗费大量时间。  
  
### <a name="to-power-off-the-appliance"></a>若要关闭设备电源  
  
> [!WARNING]  
> 必须按所列的确切顺序执行所有步骤，每个步骤之前，必须完成都执行下一步，除非另有说明。 执行顺序不正确或无需等待每个步骤才能完成的步骤会导致错误，当设备在更高版本时已启动。  
  
1.  连接到 PDW 控制节点 (***PDW_region *-CTL01** )，并使用分析平台系统 appliance 域管理员帐户登录。  
  
2.  运行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`以打开**Configuration Manager**。  
  
3.  在配置管理器下**并行数据仓库拓扑**菜单上，单击**服务状态**选项卡，然后单击**停止区域**停止 PDW 服务。   
  
4.  连接到 ***appliance_domain *-HST01** ，并使用设备域管理员帐户登录。  
  
5.  使用**故障转移群集管理器**连接到 ***appliance_domain *-WFOHST01**群集，如果不会自动连接，然后在导航窗格中，依次**角色**. 在中**角色**窗格：  
  
    1.  多重选择所有的虚拟机。 右键单击它们，然后选择**关机**。  
  
    2.  等待完成关闭所选的所有 Vm。  
  
6.  关闭**故障转移群集管理器**应用程序。  
  
7. 关闭所有的服务器除外 ***appliance_domain *-HST01**。  
  
8. 关闭 ***appliance_domain *-HST01**服务器。  
  
9. 关闭配电装置 (Pdu)。  
  
## <a name="PowerOn"></a>在设备上的电源  
  
### <a name="to-power-on-the-appliance"></a>若要打开设备电源  
  
> [!WARNING]  
> 必须按所列的确切顺序执行所有步骤，每个步骤之前，必须完成都执行下一步，除非另有说明。 执行步骤顺序不正确或无需等待完成每个步骤可能会导致启动错误。  
  
1.  打开电源配电装置 (PDU)，并等待切换为自动启动。  
  
2.  开启 ***appliance_domain *-HST01**服务器。  
  
3.  登录到 ***appliance_domain *-HST01**以设备域管理员。  
  
4.  启动**Hyper-v 管理器**程序 (**virtmgmt.msc**) 并连接到 ***appliance_domain *-HST01**如果默认情况下未连接。  
  
    1.  如果由于不能按名称连接 ***PDW_region *-AD01**是未运行，请尝试使用的 IP 地址连接。  
  
    2.  在中**虚拟机**窗格中，找到 ***PDW_region *-AD01**并确认它正在运行。 如果不是，启动此虚拟机，并等待它完成启动。  
  
5.  打开设备中的服务器的其余部分。  
  
6.  位于**HST01**上记录作为设备域管理员，从**Hyper-v 管理器**:  
  
    1.  连接到 ***appliance_domain *-HST02**。  
  
    2.  在中**虚拟机**窗格中，找到 ***PDW_region *-AD02**并确认它正在运行。  如果不是，启动此虚拟机，并等待它完成启动。  
  
7.  使用**故障转移群集管理器**连接到 ***appliance_domain *-WFOHST01**群集，如果不会自动连接，然后在**导航**窗格中，单击**角色**。 在中**角色**窗格：  
  
    1.  多选的所有虚拟机中，右键单击它们，然后依次**启动**。  
  
    2.  等待所有所选 Vm 完成启动之前继续执行下一步。  
  
    3.  如有必要为虚拟机在故障转移后，将其关闭、 移动它们，和正确的主要主机上重新启动它们。  
  
8. 断开**HST01**如果您想。  
  
9. 连接到 ***PDW_region *-CTL01**使用设备域管理员帐户。  
  
10. 运行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`以启动**Configuration Manager**。  
  
11. 在中**Configuration Manager**，在**并行数据仓库拓扑**菜单中，单击**服务状态**选项卡，然后单击**启动区域**启动 PDW 服务。  
  
### <a name="to-verify-the-appliance-health"></a>若要验证设备运行状况  
启动设备后，打开**管理员控制台**并检查可能指明故障条件的警报的运行状况页。 有关详细信息，请参阅[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。  
  
## <a name="see-also"></a>请参阅  
[设备管理任务&#40;分析平台系统&#41;](appliance-management-tasks.md)  
  
