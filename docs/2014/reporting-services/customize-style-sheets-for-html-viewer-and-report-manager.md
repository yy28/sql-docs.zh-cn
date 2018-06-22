---
title: 为 HTML 查看器和报表管理器自定义样式表 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- style sheets [Reporting Services]
ms.assetid: df805cff-b1de-4062-b2ac-423f37390fbd
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: b24525eff885b183b34f5810d79e44e4509e3f06
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014970"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>自定义 HTML 查看器和报表管理器的样式表
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供默认级联样式表 (.css) 文件的定义样式**报表**HTML 查看器中和报表管理器的工具栏。 如果您是 Web 开发人员或具备创建级联样式表的专业知识，则可以修改默认样式，以更改工具栏或报表管理器的颜色、字体和布局，但需自行承担相应的风险。 此版本中既没有记录默认样式表，也没有记录修改样式表的说明。  
  
 不正确地修改样式表可能会导致在打开报表时出现错误。 如果您不知道如何修改样式表，则应使用默认样式表。 如果您选择自定义样式表，则请务必在进行任何修改之前，创建所有默认 .css 文件的备份。  
  
 修改样式表不会对在报表服务器上运行的已发布报表的外观产生任何影响。 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中，报表不引用样式表。 由报表服务器自动生成的特别报告使用作为嵌入资源存储于报表服务器程序文件中的样式信息。 在报表设计器中创建的报表将使用您在报表定义中指定的字体、颜色和布局。 将创建与布局的其余部分内联的样式。  
  
> [!NOTE]  
>  如果要使用预定义的报表样式，则请使用报表向导来创建报表。 报表向导提供了各种主题，可用于创建使用不同颜色组合和字体的样式化报表。 可以修改定义报表主题的样式模板。  
  
## <a name="reporting-services-style-sheets"></a>Reporting Services 样式表  
 下表描述在中使用的样式表 (.css) 文件[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]安装。  
  
|样式表|Description|  
|-----------------|-----------------|  
|Htmlviewer.css|提供可用作模板的示例样式表，为 HTML 查看器中的 **“报表”** 工具栏创建自定义样式。<br /><br /> HTML 查看器使用的默认样式已编译到报表服务器上。 Htmlviewer.css 文件提供了查看器使用的样式示例。|  
|ReportingServices.css|为报表管理器定义样式。|  
  
> [!NOTE]  
>  下列样式表用于报表管理器联机文档，并且在任何时候都不应该修改：Sql.css 和 Mailto.css。 其他样式表为在 SharePoint Web 部件中打开的报表和报表管理器定义样式。 这些样式表包括 Rswebparts.css、Sp_full.css 和 Sp_small.css。 建议不要修改 SharePoint 样式表。 有关如何使用 Web 部件的详细信息，请参阅[视图和浏览本机模式报表使用 SharePoint Web 部件&#40;SSRS&#41;](reports/view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs.md)。  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>将 Reporting Services 配置为使用自定义样式表  
 样式表必须是有效的级联样式表 (.css) 文件，并且必须位于 Styles 文件夹中。 默认情况下，样式文件夹位于\<*驱动器*>: files\microsoft SQL Server\MSSQL。*n*\Reporting Services\ReportServer\Styles。  
  
 若要在运行时使用自定义的 HTML 查看器样式表，可以从下列方法中进行选择：  
  
-   将 <`HTMLViewerStyleSheet`> 设置添加到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 配置文件中。  
  
-   在报表 URL 上指定样式表。  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.config 文件  
 您可以修改 RSReportServer.config 文件以便为 HTML 查看器指定自定义样式表。 默认情况下，该文件中不包含 <`HTMLViewerStyleSheet`> 设置。 您必须将此设置键入到 RSReportServer.config 文件的 <`Configuration`> 选项中，然后指定要使用的样式表。 指定样式表时，请不要包括 .css 文件扩展名。  
  
 下面的示例对如何指定样式表进行了说明：  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>在报表 URL 上指定样式表  
 您可以使用 `rc:StyleSheet` URL 访问参数在报表 URL 上指定自定义样式表。 有关如何指定 URL 访问参数的详细信息，请参阅[URL Access Parameter Reference](url-access-parameter-reference.md)。  
  
 下面的示例对如何添加自定义样式进行了说明：  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>请参阅  
 [报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [HTML 查看器和报表工具栏](html-viewer-and-the-report-toolbar.md)   
 [RSReportServer 配置文件](report-server/rsreportserver-config-configuration-file.md)  
  
  