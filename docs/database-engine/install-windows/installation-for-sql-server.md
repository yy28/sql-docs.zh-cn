---
title: SQL Server 安装 | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: install
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 59eb3b4f64e0eaa4b40f51df98ee3db8057be3f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-installation"></a>SQL Server 安装 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导提供一个功能树以用来安装所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
-   连接组件  
  
从 [!INCLUDE[ss2016](../../includes/sssql15-md.md)] 开始，SQL Server 管理工具不再从主功能树安装；有关详细信息，请参阅[下载 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)  
  
您可以单独安装每个组件，也可以选择上面列出的组件的组合。 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的不同版本和可用组件中做出最佳选择，请查看你的 SQL Server 版本支持的功能：

- [[!INCLUDE[ss2017](../../includes/sssqlv14-md.md)] 的各版本和支持的功能](~/sql-server/editions-and-components-of-sql-server-2017.md)。  
- [[!INCLUDE[ss2016](../../includes/sssql15-md.md)] 的各版本和支持的功能](~/sql-server/editions-and-components-of-sql-server-2016.md)。  
- [[!INCLUDE[ss2014](../../includes/sssql14-md.md)] 各版本支持的功能](http://technet.microsoft.com/library/cc645993(v=sql.120).aspx)
  
## <a name="in-this-section"></a>本节内容  
无论使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导还是命令提示符安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，安装都包括下列步骤：  
  
[计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)  
说明如何为安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]而准备计算机：  
  
-   硬件和软件要求。  
-   系统配置检查器的要求和妨碍性问题。  
-   安全注意事项。  
  
[安装 SQL Server](../../database-engine/install-windows/install-sql-server.md)  
 说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的安装选项。  
  
[SQL Server 安装程序的用户界面参考](http://msdn.microsoft.com/library/183b5cdd-962e-41ca-8064-ea44f622c77d)  
 说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导提供的安装选项。  
  
[升级 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 介绍用于升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的选项。  
  
[卸载 SQL Server](../../sql-server/install/uninstall-sql-server.md)  
 说明卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的过程。  
  
[SQL Server 故障转移群集安装](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本节介绍了如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集。  
  
[安装 SQL Server Business Intelligence 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft BI 平台的部分功能包括： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，以及用于创建或使用分析数据的若干客户端应用程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本节说明如何安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
## <a name="more-information"></a>详细信息
[使用 SharePoint 安装 SQL Server BI 功能（Power Pivot 和 Reporting Services）](http://msdn.microsoft.com/library/3166107c-30c2-468e-bb1b-bb42b79b37c3)  
 本节介绍如何在 SharePoint 环境中安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 它标识对于特定版本的 SharePoint，提供了哪些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 本节还包含在 SharePoint 模式下安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 和 Reporting Services 的过程。  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) 安装新的示例数据库 [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)。 
  
[其他 SQL Server 示例和示例数据库](http://sqlserversamples.codeplex.com/)  
 说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 示例和示例数据库。  
  
有关所有 [受支持版本的链接和信息，请参阅](https://msdn.microsoft.com/library/ff803383.aspx) SQL Server 更新中心 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 安装中的新增功能](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
[安装 SQL Server 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
