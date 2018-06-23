---
title: 工具和 Analysis Services 中使用的应用程序 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cb258b1d1cc9466d1b1c88255e6edbbb854b5aef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027316"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>在 Analysis Services 中使用的工具和应用程序
  找到您将需要用于生成 Analysis Services 模型以及用于在 Analysis Services 实例上管理关联数据库的工具和应用程序。  
  
## <a name="analysis-services-model-designers"></a>Analysis Services 模型设计器  
 表格和多维模型是从 Visual Studio shell 内部生成的一个解决方案中的项目模板创建。 项目模板提供用于创建模型、多维数据集、维度和包含 Analysis Services 解决方案的角色的设计器。  
  
### <a name="download-sql-server-data-tools-for-business-intelligence-ssdt-bi"></a>下载 SQL Server Data Tools for Business Intelligence (SSDT-BI)  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] for Business Intelligence (SSDT-BI)（以前称为 Business Intelligence Development Studio (BIDS)）用于创建 Analysis Services 模型、Reporting Services 报表和 Integration Services 包。 您可以从以下位置下载 SSDT-BI：  
  
-   [下载 SSDT BI for Visual Studio 2013](http://go.microsoft.com/fwlink/p/?LinkId=396526)  
  
-   [下载 SSDT BI for Visual Studio 2012](http://go.microsoft.com/fwlink/p/?LinkID=273673)  
  
 如果计算机上装有旧版 SSDT-BI 或 BIDS，则新版与旧版并行安装。 在一个工作站上同时运行新版和旧版的设计工具是很常见的，这样可以修改与特定服务器版本关联的项目和解决方案。  
  
> [!NOTE]  
>  有多个下载站点可下载 SSDT 的 Visual Studio 2012 和 Visual Studio 2013 版本。 大多不含 BI 项目模板。 使用上面的链接可获得正确的版本。 如果看到 Business Intelligence 项目模板文件夹，即说明 SSDT-BI 的版本正确无误。 此文件夹包含 Analysis Services、Reporting Services 和 Integration Services 的项目模板。 根据安装 SSDT-BI 的方式，可能还会看到一个 SQL Server 数据库项目模板。  
  
 ![SSDT 中新的项目模板](media/ssdt-biprojects.png "New Project templates in SSDT")  
  
## <a name="administrative-tools"></a>管理工具  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Management Studio 是所有 SQL Server 功能（包括 Analysis Services）的主要管理工具。 SQL Server Management Studio 是可选组件。 如果你在 Windows Server 2012 的应用程序页面上未看见该组件与其他 SQL Server 应用程序一并列出，则运行 SQL Server 安装程序，将其添加到你的安装中。  
  
### <a name="sql-server-profiler"></a>SQL Server 事件探查器  
 SQL Server Profiler 提供一种便捷方法，用以监视连接、MDX 查询执行和其他服务器操作，但从官方角度来说，不推荐使用此方法。 SQL Server Profiler 将按默认安装。 可在 Windows Server 2012 中的应用程序上一并找到此组件与 SQL Server 应用程序。  
  
### <a name="powershell"></a>PowerShell  
 可以使用 PowerShell 命令执行许多管理任务。 有关详细信息，请参阅 [Analysis Services PowerShell](analysis-services-powershell.md) 。  
  
### <a name="community-and-third-party-tools"></a>社区和第三方工具  
 检查 [Analysis Services codeplex 页面](http://sqlsrvanalysissrvcs.codeplex.com/) 是否具有社区代码示例。 当寻求对支持 Analysis Services 的第三方工具的推荐时，可在[论坛](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) 获得帮助。  
  
  