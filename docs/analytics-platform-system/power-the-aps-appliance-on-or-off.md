---
title: "Power AP 设备打开或关闭 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2258f8e3-e7a1-4455-8a5e-10d4d15775d6
caps.latest.revision: "45"
ms.openlocfilehash: 3264c3f97f765e9a62a38987638bdf2a8b13e82b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="power-the-aps-appliance-on-or-off"></a>打开或关闭电源 AP 设备
本主题介绍如何开启或关闭你分析平台 Systemappliance 运行并行数据仓库，并根据需要运行的 HDInsight 区域。 使用本主题时移动分析平台系统设备，或 power 在设备上灾难性电源发生故障后。  
  
打开和关闭电源设备不与启动和停止设备服务相同。 有关该主题的信息，请参阅[PDW 服务状态 &#40;分析平台系统 &#41;](pdw-services-status.md). 有关电源打开或关闭 SQL Server 2008 并行数据仓库的信息，请参阅 SQL Server 2008 并行数据仓库帮助文件。 有关电源打开或关闭 SQL Server 2012 AU1 或 AU2 并行数据仓库的信息，请参阅这些版本的帮助文件。  
  
当这些说明指定连接到 SQL Server PDW 节点时，可以本地使用附加的设备 (KVM) 连接或远程使用远程桌面。 （电电源开关） 的物理内存和一些模块 （如关闭），必须向某些操作可以是物理或通过使用 Windows 的命令。  
  
可以使用分配给节点，或从分配的 IP 地址建立到 SQL Server PDW 节点的连接**HST01**计算机通过使用**故障转移群集管理器**(**cluadmin.msc**)或**Hyper-v 管理器**(**virtmgmt.msc**) 应用程序，然后右键单击节点名称。  
  
## <a name="PowerOff"></a>关闭设备电源  
  
### <a name="before-you-begin"></a>开始之前  
关闭设备电源之前, 应结束设备上的所有活动。 若要结束所有活动：  
  
-   使用**会话**管理员控制台来标识当前用户的页。 与他们联系，要求他们需要注销。  
  
-   如果必要您可以使用**终止**强制客户端连接终止的语句。 终止时要格外小心连接。 时中断，某些事务的进程，如长时间运行的更新，必须在 SQL Server 之前回滚活动可以完成恢复的数据库。 回滚已部分完成的 update 或 delete，可能会非常耗时。  
  
### <a name="to-power-off-the-appliance"></a>关闭设备电源  
  
> [!WARNING]  
> 必须按列出的确切顺序执行所有步骤和每个步骤之前，必须完成都执行下一步，则除非另行说明。 在更高版本时的设备已启动时，则将执行顺序不正确或而无需等待每个步骤来完成的步骤会导致错误。  
  
1.  连接到 PDW 控制节点 (***PDW_region*-CTL01** )，用 Analytics Platform System 设备域管理员帐户登录。  
  
2.  运行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`以打开**Configuration Manager**。  
  
3.  在 Configuration Manager 中，在**并行数据仓库拓扑**菜单上，单击**服务状态**卡，然后单击**停止区域**停止 PDW 服务。  
  
4.  如果下的 HDInsight 区域中， **HDInsight 拓扑**菜单上，单击**服务状态**卡，然后单击**停止区域**停止 HDInsight 服务。  
  
5.  连接到 ***appliance_domain*-HST01** ，用设备域管理员帐户登录。  
  
6.  使用**故障转移群集管理器**连接到 ***appliance_domain*-WFOHST01**群集，如果不自动连接，，然后在导航窗格中，单击**角色**。 在**角色**窗格中：  
  
    1.  虚拟机的多项选择所有。 右键单击它们，然后选择**关机**。  
  
    2.  等待所有所选的虚拟机，若要完成的情况下关闭。  
  
7.  如果没有 HDInsight 区域：  
  
    1.  连接到 HDInsight 群集。 若要执行此操作，右键单击**故障转移群集管理器**，选择**连接到群集**，并指定 ***appliance_domain*-WFOHST02**为群集名称。  
  
    2.  在 HDInsight 群集中，单击**角色**。 在**角色**窗格中：  
  
        1.  多选择的所有虚拟机中，右键单击它们，并选择**关机**。  
  
        2.  等待要关闭的虚拟机。  
  
8.  关闭**故障转移群集管理器**应用程序。  
  
9. 关闭所有的服务器除外 ***appliance_domain*-HST01**。  
  
10. 关闭 ***appliance_domain*-HST01**服务器。  
  
11. 关闭配电装置 (Pdu)。  
  
## <a name="PowerOn"></a>在设备上的电源  
  
### <a name="to-power-on-the-appliance"></a>在设备上的电源  
  
> [!WARNING]  
> 必须按列出的确切顺序执行所有步骤和每个步骤之前，必须完成都执行下一步，则除非另行说明。 执行顺序不正确或而无需等待每个步骤来完成的步骤可能导致启动错误。  
  
1.  打开电源配电装置 (PDU)，并等待开关为自动启动。  
  
2.  开启 ***appliance_domain*-HST01**服务器。  
  
3.  登录到 ***appliance_domain*-HST01**作为设备域管理员。  
  
4.  启动**Hyper-v 管理器**程序 (**virtmgmt.msc**) 并连接到 ***appliance_domain*-HST01**如果默认情况下未连接。  
  
    1.  如果你无法连接的名称，因为 ***PDW_region*-AD01**是未在运行，请尝试使用的 IP 地址连接。  
  
    2.  在**虚拟机**窗格中，找到 ***PDW_region*-AD01**并确认它正在运行。 如果没有，启动此虚拟机，然后等待它完成启动。  
  
5.  剩余的设备中的服务器上的电源。  
  
6.  在**HST01**从设备域管理员身份，登录**Hyper-v 管理器**:  
  
    1.  连接到 ***appliance_domain*-HST02**。  
  
    2.  在**虚拟机**窗格中，找到 ***PDW_region*-AD02**并确认它正在运行。  如果没有，启动此虚拟机，然后等待它完成启动。  
  
7.  使用**故障转移群集管理器**连接到 ***appliance_domain*-WFOHST01**群集，如果不自动连接，然后在**导航**窗格中，单击**角色**。 在**角色**窗格中：  
  
    1.  所有虚拟机中，右键单击它们，并依次选择多**启动**。  
  
    2.  等待所有所选的虚拟机，若要完成启动然后再继续下一步。  
  
    3.  如有必要的故障转移的 Vm，关闭它们、 将它们，移动和正确的主要主机上重新启动它们。  
  
8.  如果该装置了 HDInsight 区域，连接到 HDInsight 群集。 (若要执行此操作，右键单击**故障转移群集管理器**，选择**连接到群集**，并指定 ***appliance_domain*-WFOHST01**群集名称。）  
  
    1.  在 HDInsight 群集中，单击**角色**。 在**角色**窗格。  
  
        1.  多选择的所有虚拟机中，右键单击它们，并选择**启动**，  
  
        2.  等待所有所选的虚拟机，若要完成启动然后再继续下一步。  
  
        3.  如果为虚拟机故障转移，有必要，请关闭它们、 将它们移和正确的主要主机上重新启动它们。  
  
9. 断开**HST01**如果你想。  
  
10. 连接到 ***PDW_region*-CTL01**使用设备域管理员帐户。  
  
11. 运行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`以启动**Configuration Manager**。  
  
12. 在**Configuration Manager**中**并行数据仓库拓扑**菜单上，单击**服务状态**卡，然后单击**启动区域**启动 PDW 服务。  
  
13. 如果设备具有 HDInsight 区域，在 HDInsight 拓扑菜单中，单击**服务状态**卡，然后单击**启动区域**启动 HDInsight 服务。  
  
### <a name="to-verify-the-appliance-health"></a>若要验证的设备运行状况  
设备已开始后，打开**管理控制台**并检查可能指明故障条件的警报的运行状况页。 有关详细信息，请参阅[使用管理控制台 &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>另请参阅  
[设备管理任务 &#40;分析平台系统 &#41;](appliance-management-tasks.md)  
  
