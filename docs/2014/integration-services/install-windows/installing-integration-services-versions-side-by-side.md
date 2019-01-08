---
title: 互操作性和共存 (Integration Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0af7cfe8119c6ceb879c75ffee4497e62997f77f
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53355886"
---
# <a name="interoperability-and-coexistence-integration-services"></a>互操作性和共存 (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services (SSIS) 可与 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 并存。  
  
## <a name="features-and-differences"></a>功能和区别  
 下表列出了 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]当前版本与早期版本之间的一些区别。  
  
|功能|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|开发环境|[SQL Server 2014 Data Tools-Business Intelligence for Visual Studio 2012 CTP 2](https://www.microsoft.com/download/details.aspx?id=40736)<br /><br /> [SQL Server 2014 Data Tools-Business Intelligence for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools for Visual Studio 2010](https://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools-Business Intelligence for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|管理环境|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|msdb 中用于存储包的主系统表|sysssispackages|sysssispackages|sysssispackages|  
|用于运行包的主命令提示实用工具|**dtexec** (dtexec.exe)，2014 版|**dtexec** (dtexec.exe), 2012 版|**dtexec** (dtexec.exe), 2008 版|  
|默认根文件系统文件夹|C:\Program Files\Microsoft SQL Server\120\DTS|C:\Program Files\Microsoft SQL Server\110\DTS|C:\Program Files\Microsoft SQL Server\100\DTS|  
|默认根注册表项|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>并存兼容性问题  
 将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 与 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 并行安装后，即可执行以下任务：  
  
-   **在 SQL Server Data Tools 中设计包**。 您使用以下工具基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相应版本开发和维护包。  
  
    -   使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本的 Business Intelligence Development Studio 开发和维护基于 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 的包。  
  
    -   使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 开发和维护基于 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]的包。  
  
    -   使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 开发和维护基于 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]的包。  
  
-   **加载和运行包**。 可以在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中加载和运行在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中开发的包。 将包添加到一个现有项目时，该包将永久升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开包文件时，该包将暂时升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式。 如果您保存对该包的更改，该包将永久升级。 一旦保存为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式，包将再也无法在相应 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本的 Business Intelligence Development Studio 中打开，也无法通过相应的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 工具运行。  
  
-   **在 SQL Server Management Studio 中管理包**。 您无法通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 版本的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 连接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]服务。 您无法通过 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]服务。 您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 管理在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的实例中存储的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]包。 您需要修改服务配置文件，以便将 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 实例添加到由服务管理的位置列表中。 有关详细信息，请参阅 [配置 Integration Services 服务（SSIS 服务）](../service/integration-services-service-ssis-service.md)的早期版本向后兼容。  
  
-   **在 SQL Server 中存储包**。 您可以在以下数据库中存储包。  
  
    |包格式|“数据库”|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 集成服务|实例的 msdb 数据库 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 集成服务|实例的 msdb 数据库 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 集成服务|实例的 msdb 数据库 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     对于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例，可以从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 实例或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]实例导入包，但不能将包导出到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 实例或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]实例。  
  
     对于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 实例或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]实例，不能从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例导入包，也不能将包导出到该实例。  
  
-   **运行包**。 可以使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 实用工具或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 **dtexec** Integration Services 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services 包。 每当 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 工具加载在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中开发的包时，该工具都会在内存中将包临时转换为 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 使用的包格式。 如果 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 包存在导致无法成功转换的问题，则在解决这些问题之前， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 工具将无法运行该包。 有关详细信息，请参阅 [Upgrade Integration Services Packages](upgrade-integration-services-packages.md)。  
  
  
