---
title: 互操作性和共存 (Integration Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f7face1f41fdf02f772c05427db9d45d1bd6050
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277583"
---
# <a name="interoperability-and-coexistence-integration-services"></a>互操作性和共存 (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services (SSIS) 可同时存在与并行[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Integration Services 和[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Integration Services。  
  
## <a name="features-and-differences"></a>功能和区别  
 下表列出了 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 当前版本与早期版本之间的一些区别。  
  
|功能|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|开发环境|[SQL Server 2014 Data Tools – Business Intelligence for Visual Studio 2012 CTP 2](http://www.microsoft.com/download/details.aspx?id=40736)<br /><br /> [SQL Server 2014 Data Tools-Business Intelligence for Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools for Visual Studio 2010](http://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools – Business Intelligence for Visual Studio 2012](http://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|管理环境|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|msdb 中用于存储包的主系统表|sysssispackages|sysssispackages|sysssispackages|  
|用于运行包的主命令提示实用工具|**dtexec** (dtexec.exe)，2014 版|**dtexec** (dtexec.exe), 2012 版|**dtexec** (dtexec.exe), 2008 版|  
|默认根文件系统文件夹|C:\Program Files\Microsoft SQL Server\120\DTS|C:\Program Files\Microsoft SQL Server\110\DTS|C:\Program Files\Microsoft SQL Server\100\DTS|  
|默认根注册表项|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>并存兼容性问题  
 将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 与 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 并行安装后，即可执行以下任务：  
  
-   **在 SQL Server Data Tools 中设计包**。 您使用以下工具基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的相应版本开发和维护包。  
  
    -   使用[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Business Intelligence Development Studio 来开发和维护基于包的版本 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]  
  
    -   使用[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]新版[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]开发和维护包基于[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]。  
  
    -   使用[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新版[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]开发和维护包基于[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]。  
  
-   **加载和运行包**。 您可以加载和运行中开发的包[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]并[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 将包添加到一个现有项目时，该包将永久升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中打开包文件时，该包将暂时升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式。 如果您保存对该包的更改，该包将永久升级。 一次保存格式的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Integration Services 使用，包可以不再打开中的相应[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]版本的 Business Intelligence Development Studio，也不由相应的运行[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Integration Services 或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Integration Services 工具。  
  
-   **在 SQL Server Management Studio 中管理包**。 无法连接到的实例[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新版[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服务，从[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]版本[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 无法连接到的实例[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]新版[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服务[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 管理在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的实例中存储的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包。 您需要修改服务配置文件，以便将 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 实例添加到由服务管理的位置列表中。 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](../service/integration-services-service-ssis-service.md)。  
  
-   **在 SQL Server 中存储包**。 您可以在以下数据库中存储包。  
  
    |包格式|“数据库”|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 集成服务|实例的 msdb 数据库 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 集成服务|实例的 msdb 数据库 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 集成服务|实例的 msdb 数据库 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     实例上[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，可以将导入包的实例[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的实例或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，但不能将包导出到的实例[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或实例的[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
     对于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 实例或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 实例，不能从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例导入包，也不能将包导出到该实例。  
  
-   **运行包**。 可以运行[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Integration Services 和[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过使用 Integration Services 包[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新版**dtexec**实用程序或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理。 每当[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Integration Services 工具加载了开发中的包[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，该工具暂时转换，在内存中时，对包的包格式[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]使用。 如果[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]包存在问题，无法成功转换， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 工具将这些问题解决之前无法运行包。 有关详细信息，请参阅 [Upgrade Integration Services Packages](upgrade-integration-services-packages.md)。  
  
  
