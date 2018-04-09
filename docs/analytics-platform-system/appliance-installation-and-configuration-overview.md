---
title: 设备安装和配置概述 （分析平台系统）
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10934f62-4acf-4ca5-b550-f426ba81fe11
caps.latest.revision: 23
ms.openlocfilehash: df27bb16f24e313f7cb1d7c7f5ced912c0a09e1d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="appliance-installation-and-configuration-overview"></a>设备安装和配置概述
SQL Server PDW 设备管理员通过设置和开始使用新的 SQL Server PDW 设备的初始步骤将指导。  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1.安装的硬件  
在数据中心停靠的托盘将提供新的设备。  
  
> [!IMPORTANT]  
> 在某些情况下，你 IHV 将解压缩、 机架，并在数据中心中为你连接设备。 如果这样，这些说明将不再需要，可以跳到[3。将设备配置为](#ConfigureAppliance)下面一节。  
  
如果你 IHV 不执行硬件安装时，使用以下步骤安装硬件。  
  
|||  
|-|-|  
|**任务**|**Description**|  
|确认文档|确认你已从你的独立硬件供应商 (IHV) 接收所有必要的文档和信息。 请参阅[信息以获得你 IHV &#40;Analytics Platform System&#41;](information-to-obtain-from-your-ihv.md)。|  
|安装硬件|验证数据中心可以容纳设备。 将设备组件移到数据中心中。 机架的网络交换机，Pdu，和电缆。 请参阅[硬件安装&#40;Analytics Platform System&#41;](hardware-installation.md)。|  
  
## <a name="PowerOnAppliance"></a>2.在设备上的电源  
  
|||  
|-|-|  
|**任务**|**Description**|  
|在设备上的电源|按要求的顺序，根据需要进行确认，未遇到任何错误等待每个设备组件节点上的电源。|  
  
## <a name="ConfigureAppliance"></a>3.配置设备  
  
|||  
|-|-|  
|**任务**|**Description**|  
|||  
|将设备配置通过使用 SQL Server PDW**Configuration Manager**|使用配置管理器在你的设备上设置设备密码、 时区、 网络和防火墙设置、 安全证书和性能和其他设置。 请参阅[设备配置&#40;Analytics Platform System&#41;](appliance-configuration.md)。|  
  
> [!WARNING]  
> 仅应使用 SQL Server PDW 进行配置更改**Configuration Manager**。 更改不通过公开**Configuration Manager**不支持。 例如，SQL Server PDW 设备仅支持美国英语语言设置。  
  
## <a name="SoftwareServicing"></a>4.设置软件维护  
  
|||  
|-|-|  
|**任务**|**Description**|  
|将 SQL Server PDW 更新应用|（可选）你可能需要应用一个或多个 SQL Server PDW 更新，以将你的 SQL Server PDW 软件更新到最新版本。 请参阅[应用分析平台系统修补程序&#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)。|  
|配置 Windows Server Update Services|配置设备以接收来自 Windows Server Update Services 以支持软件更新。 请参阅[下载并应用 Microsoft 更新&#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)。|  
  
## <a name="NextSteps"></a>后续步骤  
完成所有前面的步骤后，你的设备可供使用。 你或你的位置处的其他人员可以继续执行以下任务。  
  
|||  
|-|-|  
|**任务**|**Description**|  
|安装 SQL Server PDW 驱动程序和配置连接|配置本地计算机以使用 SQL Server Data Tools、 sqlcmd、 业务智能软件或其他工具连接到 SQL Server PDW。 <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|创建登录和服务器角色，并分配权限|规划并创建将允许用户登录到 SQL Server PDW 具有相应权限的登录和服务器角色。 <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|配置 Azure 数据管理网关|网关使 Azure 用户能够访问本地 AP 数据通过公开 AP 数据尽可能的安全 OData 馈送。 网关已安装在管理节点上。 Microsoft 寻求使用配置的帮助。|  
|监视器查询和设备用户|使用管理控制台和其他资源来监视查询和设备的用户。 请参阅[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->。|  
|将数据加载到 SQL Server PDW|将数据加载到你的设备。 <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|创建灾难恢复计划|规划如何将保护你的数据从硬件故障或数据覆盖。 创建计划使用定期备份和还原在出现数据损坏或丢失的计划。 <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|监视设备|使用系统视图、 日志和管理控制台监视设备状态、 运行状况和性能。 更正或报告的任何问题。 请参阅[监视器设备运行状况状态&#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。|  
