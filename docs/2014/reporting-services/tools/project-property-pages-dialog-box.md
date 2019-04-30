---
title: “项目属性页”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rpt.rptdesigner.projectpropertypages.general.f1
helpviewer_keywords:
- Project Property Pages dialog box
ms.assetid: 209d9e22-37fc-418f-8739-83adcf447d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a76281eead6430ca0dafae8671c7990f3c6c2de3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63201075"
---
# <a name="project-property-pages-dialog-box"></a>“项目属性页”对话框
  使用项目属性页可以配置报表服务器项目的部署属性。 若要打开此对话框，请在“项目”菜单中，单击“\<报表项目名称>属性”。  
  
 定义配置属性后，可以从位于工具栏上的“解决方案配置”下拉列表中选择配置。  
  
## <a name="options"></a>选项  
 **Configuration**  
 选择要编辑的配置。 最初，并提供以下配置：**调试**， **DebugLocal**，和**发行**。 首先显示活动配置，例如 **Active(Debug)**。  
  
 若要同时查看多个配置的属性，请选择 **“所有配置”** 或 **“多个配置”**。  
  
 若要创建其他配置，请单击工具栏上的 **“配置管理器”** 。  
  
 **“配置管理器”**  
 管理整个解决方案的配置或添加其他配置。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 文档。  
  
 **OutputPath**  
 键入或粘贴用于存储在报表生成验证、部署和预览过程中使用的报表定义的路径。 此路径必须与您用于项目的路径不同，并且它是一个相对路径（即项目路径下的一个子文件夹）。  
  
> [!NOTE]  
>  可以使用多个配置，以便根据您执行的任务在路径间切换。  
  
 **ErrorLevel**  
 键入报告为错误的生成问题的严重性。 严重级别小于或等于 **ErrorLevel** 的值的问题将报告为错误；否则，将问题报告为警告。 任何错误都将导致生成任务失败。 有效的严重级别为 0 到 4（包括这两者）。 默认值为 2。  
  
 **StartItem**  
 选择在项目发布到报表服务器之后将显示在 Web 浏览器中的报表，或选择在本地运行项目时将显示在预览窗口中的报表。 对于生成项目但并不部署项目的配置，以及使用 **Debug** 命令 (**F5**)，启动项是必需的。 对于部署项目的配置，启动项也是必需的。  
  
 **OverwriteDataSources**  
 选择 **True** 可在发布报表时使用项目中的数据源覆盖服务器上的数据源。 选择 **False** 可保留服务器上的现有数据源。  
  
 **TargetServerVersion**  
 选择任一[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]新版[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]或选择**检测版本**来自动确定标识的服务器上安装的版本**TargetServer URL**属性。 默认值为 **SQL Server 2008 R2**。  
  
 **TargetDataSourceFolder**  
 要在其中存储已发布共享数据源的文件夹的名称。 如果您没有指定文件夹，那么数据源将发布到与报表所在文件夹相同的文件夹。 如果报表服务器上没有该文件夹，则报表设计器将在发布报表时创建该文件夹。  
  
 发布到在本机模式下运行的报表服务器时，指定文件夹层次结构的完整路径（从根文件夹开始）。 例如，Folder1/Folder2/Folder3。  
  
 发布到在 SharePoint 集成模式下运行的报表服务器时，请使用 SharePoint 库的 URL。 例如， http://*\<服务器名 > /\<站点 >*/documents/myfolder。  
  
 **TargetReportFolder**  
 要在其中存储已发布报表的文件夹的名称。 默认情况下，此名称即为报表项目的名称。 如果报表服务器上没有该文件夹，则报表设计器将在发布报表时创建该文件夹。  
  
 发布到在本机模式下运行的报表服务器时，指定文件夹层次结构的完整路径（从根文件夹开始）。 如果文件夹位于另一个文件夹内，则包括从根目录开始的到该文件夹的路径，如 Folder1/Folder2/Folder3。  
  
 发布到在 SharePoint 集成模式下运行的报表服务器时，请使用 SharePoint 库的 URL。 例如， http://*\<服务器名 >*/*\<站点 >*/documents/myfolder。  
  
 **TargetServerURL**  
 目标报表服务器的 URL。 在发布报表之前，必须将此属性设置为有效的报表服务器 URL。  
  
 发布到在本机模式下运行的报表服务器时，请使用此报表服务器的虚拟目录 URL。 例如， http://\<服务器 > / reportserver。 这是报表服务器的虚拟目录，而不是报表管理器的虚拟目录。 默认情况下，报表服务器安装在名为“reportserver”的虚拟目录中。  
  
 发布到在 SharePoint 集成模式下运行的报表服务器时，请使用 SharePoint 顶级站点或子站点的 URL。 如果不指定站点，将使用默认顶级站点。 例如， http://\<*服务器名 >*， http://&lt*servername*/\<*站点 >* 或 http://\<*服务器名称 >*/\<*站点 >*/\<*子站点 >*。  
  
## <a name="see-also"></a>请参阅  
 [发布报表](../publish-reports.md)   
 [将报表发布到 SharePoint 库](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [设置部署属性 (Reporting Services)](set-deployment-properties-reporting-services.md)   
 [报表设计器的 F1 帮助](report-designer-f1-help.md)  
  
  
