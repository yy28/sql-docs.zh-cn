---
title: 部署和版本支持在 SQL Server Data Tools (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 36f5686d-7e40-4f31-be81-bd197ca33a02
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 15a2e200fae4f73e64faa92c3ca13b870eb68676
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040908"
---
# <a name="deployment-and-version-support-in-sql-server-data-tools-ssrs"></a>SQL Server Data Tools 中的部署和版本支持 (SSRS)
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 支持以下方案：  
  
-   打开报表定义 (*.rdl) 和报表服务器项目 (\*.rptproj)。  
  
-   生成报表定义。  
  
-   在报表设计器中预览报表。  
  
-   将报表部署到报表服务器。  
  
##  <a name="bkmk_ConfigurationandDeploymentProperties"></a> 配置和部署属性  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 支持项目配置。 项目配置由一组属性组成，当作为预览或部署报表的一个步骤生成项目时，这些属性指定位置和行为。 若要了解有关项目配置的更多信息，请参阅 Visual Studio 文档。  
  
 使用项目配置可以控制报表定义升级到与目标报表服务器兼容的架构版本。 项目配置控制的属性包括目标报表服务器、生成进程临时存储报表定义以便预览和部署的文件夹以及错误级别。  
  
 首先会生成报表，然后将其在报表设计器中以预览方式呈现，或者部署到报表服务器。  
  
 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **“项目属性”** 对话框中设置配置属性。  
  
 生成和部署属性包括：  
  
-   OutputPath 是一个生成属性，它标识用于存储在报表生成验证、部署和预览过程中使用的报表定义的文件夹路径。  
  
-   ErrorLevel 是一个生成属性，它标识报告为错误的生成问题的严重性。 严重级别小于或等于 ErrorLevel 的值的问题将报告为错误；否则，将问题报告为警告。 有关详细信息，请参阅[使用报表设计器设计报表 (SSRS)](design-reporting-services-paginated-reports-with-report-designer-ssrs.md) 中的“报表验证和错误级别”一节。  
  
-   TargetServerVersion 是一个部署属性，它标识安装在目标报表服务器（在 TargetServerURL 属性中指定）上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的预期版本。  
  
 当您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 对话框中指定早期版本的 **“项目属性”** 时，报表不会自动恢复到早期版本。 同样，报表服务器项目可以包含来自两个不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的报表。 当部署报表服务器项目时，项目中的所有报表都将转换为在 TargetServerVersion 中指定的版本。  
  
 您可以将多个项目配置添加到项目中；每个配置用于不同方案，例如，部署到不同版本的报表服务器。 有关详细信息，请参阅[设置部署属性 (Reporting Services)](set-deployment-properties-reporting-services.md) 和[“项目属性页”对话框](project-property-pages-dialog-box.md)。  
  
##  <a name="bkmk_SupportedVersions"></a> 支持的版本  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，是 32 位报表服务器项目开发环境，根据设计，它不能在基于 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]的计算机上运行，也不能在基于 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]的服务器上安装。 但是，基于 x64 的计算机可提供对 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的支持。  
  
 下表说明了可在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创作和发布报表的支持版本。  
  
> [!NOTE]  
>  架构自 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以来未更改。  
  
|项目或文件类型|版本|创作报表|发布报表|说明|  
|--------------------------|-------------|--------------------|---------------------|-----------|  
|报表服务器项目<br /><br /> 或<br /><br /> 报表服务器向导项目|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|2014 RDL 架构|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|报表服务器项目<br /><br /> 或<br /><br /> 报表服务器向导项目|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|2012 RDL 架构|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|报表服务器项目<br /><br /> 或<br /><br /> 报表服务器向导项目|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|2008 R2 RDL 架构|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|报表服务器项目<br /><br /> 或<br /><br /> 报表服务器向导项目|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|2008 RDL 架构|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器|在本地将 2003 RDL 和 2005 RDL 升级到 2008 RDL 架构。|  
|报表服务器项目<br /><br /> 或<br /><br /> 报表服务器向导项目|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|2005 RDL 架构|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]报表服务器||  
|报表服务器项目|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|2003 RDL 架构|不支持||  
|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] RDLC 报表设计器|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2005<br /><br /> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2008|2005 RDL 架构|不支持|不支持 2008 RDL 架构。|  
|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 查看器控件|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2005<br /><br /> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2008|在本地模式中不支持 2008 RDL|不可用|可以在服务器模式下查看 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器上的 2008 RDL 报表。|  
  
 有关在以前版本的报表定义架构中打开报表的详细信息，请参阅[升级报表](../install-windows/upgrade-reports.md)。 有关特定报表定义架构的详细信息，请参阅 [Report Definition Language Specification](https://go.microsoft.com/fwlink/?linkid=116865)（报表定义语言规范）。  
  
## <a name="see-also"></a>请参阅  
 [发布数据源和报表](../reports/publishing-data-sources-and-reports.md)  
  
  
