---
title: 自定义 HTML 查看器和报表管理器的样式表 |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 7c7745d69e234f81c2a331d214789e93e9fd4014
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "64568263"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>自定义 HTML 查看器和报表管理器的样式表
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]提供默认级联样式表（.css）文件，用于为 HTML 查看器中的**报表**工具栏和报表管理器定义样式。 如果您是 Web 开发人员或具备创建级联样式表的专业知识，则可以修改默认样式，以更改工具栏或报表管理器的颜色、字体和布局，但需自行承担相应的风险。 此版本中既没有记录默认样式表，也没有记录修改样式表的说明。  
  
 不正确地修改样式表可能会导致在打开报表时出现错误。 如果您不知道如何修改样式表，则应使用默认样式表。 如果您选择自定义样式表，则请务必在进行任何修改之前，创建所有默认 .css 文件的备份。  
  
 修改样式表不会对在报表服务器上运行的已发布报表的外观产生任何影响。 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中，报表不引用样式表。 由报表服务器自动生成的特别报告使用作为嵌入资源存储于报表服务器程序文件中的样式信息。 在报表设计器中创建的报表将使用您在报表定义中指定的字体、颜色和布局。 将创建与布局的其余部分内联的样式。  
  
> [!NOTE]  
>  如果要使用预定义的报表样式，则请使用报表向导来创建报表。 报表向导提供了各种主题，可用于创建使用不同颜色组合和字体的样式化报表。 可以修改定义报表主题的样式模板。  
  
## <a name="reporting-services-style-sheets"></a>Reporting Services 样式表  
 下表说明了在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安装中使用的样式表 (.css) 文件。  
  
|样式表|说明|  
|-----------------|-----------------|  
|Htmlviewer.css|提供可用作模板的示例样式表，为 HTML 查看器中的 **“报表”** 工具栏创建自定义样式。<br /><br /> HTML 查看器使用的默认样式已编译到报表服务器上。 Htmlviewer.css 文件提供了查看器使用的样式示例。|  
|ReportingServices.css|为报表管理器定义样式。|  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>将 Reporting Services 配置为使用自定义样式表  
 样式表必须是有效的级联样式表 (.css) 文件，并且必须位于 Styles 文件夹中。 默认情况下，"样式" 文件夹位于\<*驱动器*>： \Program Files\Microsoft SQL Server\MSSQL。*n*\Reporting services\reportserver\styles 中。  
  
 若要在运行时使用自定义的 HTML 查看器样式表，可以从下列方法中进行选择：  
  
-   将 <`HTMLViewerStyleSheet`> 设置添加到[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]配置文件中。  
  
-   在报表 URL 上指定样式表。  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.config 文件  
 您可以修改 RSReportServer.config 文件以便为 HTML 查看器指定自定义样式表。 默认情况`HTMLViewerStyleSheet`下，此文件中不包括 <> 设置。 您必须将其键入 Rsreportserver.config 文件`Configuration`的 <> 选择，然后指定要使用的样式表。 指定样式表时，请不要包括 .css 文件扩展名。  
  
 下面的示例对如何指定样式表进行了说明：  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>在报表 URL 上指定样式表  
 您可以使用 `rc:StyleSheet` URL 访问参数在报表 URL 上指定自定义样式表。 有关如何指定 URL 访问参数的详细信息，请参阅[Url 访问参数引用](url-access-parameter-reference.md)。  
  
 下面的示例对如何添加自定义样式进行了说明：  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [HTML 查看器和报表工具栏](html-viewer-and-the-report-toolbar.md)   
 [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)  
  
  
