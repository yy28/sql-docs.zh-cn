---
title: 安装 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: quickstart
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 43458e87144b5903a0d6436d5596bb5c3585d928
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383314"
---
# <a name="install-sql-server"></a>安装 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 从 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 开始，[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 仅可用作 64 位应用程序。 以下是有关如何获取 SQL Server 以及如何安装 SQL Server 的重要详细信息。

## <a name="installation-details"></a>安装详细信息
  
*  **选项**：通过安装向导、命令提示符或 sysprep 进行安装
 
*  **要求**：安装之前，请先查看 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md) 

* **过程**：有关安装过程的完整说明，请参阅 [安装 SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md)

* **示例数据库和示例代码**： 
    * 默认情况下，它们不作为 SQL Server 安装程序的一部分安装 
    * 若要为 SQL Server 的非 Express 版本安装它们，请参阅 [GitHub](http://github.com/Microsoft/sql-server-samples)
    

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="how-to-install-includessnoversionincludesssnoversion-mdmd"></a>如何安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]
 
|Title|描述|  
|-----------|-----------------|  
|[在服务器核心上安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-on-server-core.md)|查看本文可了解如何在 Windows Server Core 上安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]。|  
|[系统配置检查器的检查参数](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|讨论系统配置检查器 (SCC) 的功能。|  
|[使用安装向导安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]（安装程序）](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|介绍如何使用安装向导进行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 典型安装的过程文章。|  
|[通过命令提示符安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|提供运行无人参与安装的示例语法和安装参数的过程文章。|  
|[使用配置文件安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|提供通过配置文件运行安装程序的示例语法和安装参数的过程文章。|  
|[使用 SysPrep 安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|提供通过 SysPrep 运行安装程序的示例语法和安装参数的过程文章。|  
|[向 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 的实例添加功能（安装程序）](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|介绍如何更新现有 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 实例的组件的过程文章。|  
|[修复失败的 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安装](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|介绍如何修复损坏的 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安装的过程文章。|  
|[重命名托管 SQL Server 独立实例的计算机](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|介绍如何更新存储在 sys.servers 中的系统元数据的过程文章。|  
|[安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 服务更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|为 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安装更新的过程文章。|  
|[查看和读取 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|介绍如何在安装日志文件中检查错误的过程文章。|  
|[验证 SQL Server 安装](../../database-engine/install-windows/validate-a-sql-server-installation.md)|查看 SQL 发现报告的用法，以便确认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本以及在计算机上安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。|  
  
  
## <a name="how-to-install-individual-components"></a>如何安装各个组件  
  
|主题|描述|  
|-----------|-----------------|  
|[安装 SQL Server 数据库引擎](../../database-engine/install-windows/install-sql-server-database-engine.md)|说明如何安装和配置 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。|  
|[安装 SQL Server 复制](../../database-engine/install-windows/install-sql-server-replication.md)|说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制。|  
|[安装 Distributed Replay - 概述](../../tools/distributed-replay/install-distributed-replay-overview.md)|列出了有关安装 Distributed Replay 功能的文章。|  
|[安装带有 SSMS 的 SQL Server 管理工具](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具。|  
|[安装 SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|介绍安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 组件的注意事项。|  
  

## <a name="how-to-configure-sql-server"></a>如何配置 SQL Server  
  
|主题|描述|  
|-----------|-----------------|  
|[配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|本文概述了防火墙配置和 Windows 防火墙配置方法。|  
|[将多宿主计算机配置为允许 SQL Server 访问](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|本文介绍如何在多宿主环境中配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和高级安全 Windows 防火墙，以便为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例提供多个网络连接。|  
|[配置 Windows 防火墙以允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|可以按照本文中提供的步骤配置端口和防火墙设置，以允许访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或用于 SharePoint 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]。|  
  
## <a name="related-sections"></a>相关章节  
[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 的各版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[安装 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Business Intelligence 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  [SQL Server 故障转移群集安装](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>另请参阅  

[计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)   
 [升级到 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
 [卸载 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
 [高可用性解决方案 (SQL Server)](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
