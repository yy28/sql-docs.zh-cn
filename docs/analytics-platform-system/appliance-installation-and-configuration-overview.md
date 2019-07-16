---
title: 设备安装和配置的分析平台系统 |Microsoft Docs
description: 将引导完成设置和开始使用新设备的初始步骤 Analytics Platform System (APS) 设备管理员。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1f32cbeccb9a71d1d4c801443b40df5a762b8f38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961480"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>设备安装和配置分析平台系统
将引导完成设置和开始使用新设备的初始步骤 Analytics Platform System (APS) 设备管理员。  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1.安装硬件  
将新设备会传送到停靠在你的数据中心的托盘上。  
  
> [!IMPORTANT]  
> 在某些情况下，IHV 将解包、 装入机架，并为您在数据中心连接该设备。 如果存在，这些说明，则不需要，并且可以跳到[3。配置设备](#ConfigureAppliance)下面一节。  
  
如果 IHV 不执行硬件安装时，使用以下步骤安装的硬件。  
  
|||  
|-|-|  
|**任务**|**说明**|  
|确认文档|确认你已从你的独立硬件供应商 (IHV) 接收所有必要文档和信息。 请参阅[从 IHV 中获取的信息&#40;分析平台系统&#41;](information-to-obtain-from-your-ihv.md)。|  
|安装硬件|验证数据中心可以容纳多设备。 将设备组件移动到数据中心。 机架 Pdu，网络交换机和电缆线路。 请参阅[硬件安装&#40;分析平台系统&#41;](hardware-installation.md)。|  
  
## <a name="PowerOnAppliance"></a>2.在设备上的电源  
  
|||  
|-|-|  
|**任务**|**说明**|  
|在设备上的电源|打开所需的顺序，等待所需确认不遇到任何错误的每个设备组件节点的电源。|  
  
## <a name="ConfigureAppliance"></a>3.配置设备  
  
|||  
|-|-|  
|**任务**|**说明**|  
|||  
|通过使用 SQL Server PDW 配置设备**Configuration Manager**|使用配置管理器在你的设备上设置设备密码、 时区、 网络和防火墙设置、 安全证书，以及性能和其他设置。 请参阅[设备配置&#40;分析平台系统&#41;](appliance-configuration.md)。|  
  
> [!WARNING]  
> 仅应使用 SQL Server PDW 进行配置更改**Configuration Manager**。 更改不会通过公开**Configuration Manager**不受支持。 例如，SQL Server PDW 设备仅支持美国英语语言设置。  
  
## <a name="SoftwareServicing"></a>4.设置软件维护服务  
  
|||  
|-|-|  
|**任务**|**说明**|  
|将 SQL Server PDW 更新应用|（可选）您可能需要应用一个或多个 SQL Server PDW 更新来更新到最新版本的 SQL Server PDW 软件。 请参阅[应用分析平台系统的修补程序&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)。|  
|配置 Windows Server Update Services|配置设备以接收来自 Windows Server Update Services 以支持软件更新。 请参阅[下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md)。|  
  
## <a name="NextSteps"></a>后续步骤  
您已完成所有上述步骤后，你的设备是供使用。 您或您所在位置的其他人员可以继续执行以下任务。  
  
|||  
|-|-|  
|**任务**|**说明**|  
|安装 SQL Server PDW 驱动程序和配置连接|配置本地计算机以使用 SQL Server Data Tools、 sqlcmd、 商业智能软件或其他工具连接到 SQL Server PDW。 <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|创建登录和服务器角色并分配权限|规划并创建将允许用户使用适当的权限登录到 SQL Server PDW 的登录和服务器角色。 <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|配置 Azure 数据管理网关|使用网关可以 Azure 用户的本地 APS 数据访问的 AP 数据安全 OData 馈送公开。 网关已安装在控制节点上。 Microsoft 寻求配置方面的帮助。|  
|监视器通过查询和设备用户|使用管理控制台和其他资源来监视查询和设备的用户。 请参阅[通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|将数据加载到 SQL Server PDW|数据加载到你的设备。 <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|创建灾难恢复计划|规划如何将保护你的数据从硬件故障或数据覆盖。 创建计划使用定期备份和还原计划发生数据损坏或丢失时。 <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|监视设备|使用系统视图、 日志和管理控制台监视设备状态、 运行状况和性能。 请更正或报告任何问题。 请参阅[监视器装置运行状况状态更改为&#40;分析平台系统&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。|  
