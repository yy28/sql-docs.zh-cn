---
title: 安装和配置设备
description: 指导分析平台系统（AP）设备管理员完成设置并开始使用新设备的初始步骤。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 49ed0f26f20d081f4f9b307e6be90a3f5bd8c372
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942199"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>用于分析平台系统的设备安装和配置
指导分析平台系统（AP）设备管理员完成设置并开始使用新设备的初始步骤。  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="1-install-the-hardware"></a><a name="InstallHardware"></a>1. 安装硬件  
你的新设备将在托盘上交付到你的数据中心。  
  
> [!IMPORTANT]  
> 在某些情况下，你的 IHV 将为你的数据中心中的设备解包、机架并连接到你的设备。 如果是这样，则不需要这些说明，您可以跳到[3。配置设备](#ConfigureAppliance)部分。  
  
如果 IHV 未执行硬件安装，请使用以下步骤安装硬件。  
  
|任务|说明|  
|-|-|  
|确认文档|确认你已收到你的独立硬件供应商（IHV）提供的所有必需文档和信息。 请参阅[从 IHV &#40;分析平台系统&#41;获取的信息](information-to-obtain-from-your-ihv.md)。|  
|安装硬件|验证数据中心是否可以容纳该设备。 将设备组件移至数据中心。 将网络交换机、Pdu 和电缆连接在一起。 请参阅[硬件安装 &#40;分析平台系统&#41;](hardware-installation.md)。|  
  
## <a name="2-power-on-the-appliance"></a><a name="PowerOnAppliance"></a>2. 在设备上通电  
  
|任务|说明|  
|-|-|  
|开启设备|按所需顺序打开每个设备组件节点的电源，并根据需要进行确认，确认没有出现任何错误。|  
  
## <a name="3-configure-the-appliance"></a><a name="ConfigureAppliance"></a>3. 配置设备  
  
|任务|说明|  
|-|-|  
|使用 SQL Server PDW**Configuration Manager**配置设备|使用 Configuration Manager 设置设备密码、时区、网络和防火墙设置、安全证书以及设备上的其他设置。 请参阅[设备配置 &#40;分析平台系统&#41;](appliance-configuration.md)。|  
  
> [!WARNING]  
> 只应使用 SQL Server PDW**Configuration Manager**进行配置更改。 不支持通过**Configuration Manager**公开的更改。 例如，SQL Server PDW 设备仅支持美国英语的语言设置。  
  
## <a name="4-set-up-software-servicing"></a><a name="SoftwareServicing"></a>4. 设置软件服务  
  
|任务|说明|  
|-|-|  
|应用 SQL Server PDW 更新|可有可无可能需要应用一个或多个 SQL Server PDW 更新，将 SQL Server PDW 软件更新到最新版本。 请参阅[&#40;分析平台系统中应用分析平台系统修补程序&#41;](apply-analytics-platform-system-hotfixes.md)。|  
|配置 Windows Server Update Services|将设备配置为接收来自支持软件 Windows Server Update Services 的更新。 请参阅[&#40;Analytics Platform System&#41;下载并应用 Microsoft 更新](download-and-apply-microsoft-updates.md)。|  
  
## <a name="next-steps"></a><a name="NextSteps"></a>后续步骤  
完成上述所有步骤后，设备便可供使用。 你或你所在位置的其他人员可以继续执行以下任务。  
  
|任务|说明|  
|-|-|  
|安装 SQL Server PDW 驱动程序并配置连接|使用 SQL Server Data Tools、sqlcmd、商业智能软件或其他工具将本地计算机配置为连接到 SQL Server PDW。 <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|创建登录名和服务器角色，并分配权限|计划并创建登录名和服务器角色，以允许用户用适当的权限登录到 SQL Server PDW。 <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|配置 Azure 数据管理网关|使用网关，Azure 用户可以通过公开作为安全 OData 源的 AP 数据来访问本地 AP 数据。 此网关已安装在控制节点上。 要求 Microsoft 提供有关配置的帮助。|  
|监视查询和设备用户|使用管理控制台和其他资源来监视查询和设备用户。 请参阅[使用管理控制台 &#40;分析平台系统监视设备&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|将数据加载到 SQL Server PDW|将数据加载到设备。 <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|创建灾难恢复计划|规划如何保护数据免遭硬件故障或数据覆盖。 在数据损坏或丢失的情况下，使用定期备份和还原计划创建计划。 <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|监视设备|使用系统视图、日志和管理控制台监视设备状态、运行状况和性能。 更正或报告任何问题。 请参阅[监视设备运行状况状态 &#40;分析平台系统&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。|  
