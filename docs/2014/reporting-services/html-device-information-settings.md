---
title: HTML 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HTML [Reporting Services], rendering
- device information settings [Reporting Services], HTML rendering
ms.assetid: f505f478-dd6d-444a-957c-34f7cfb98911
caps.latest.revision: 47
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bb0063ac9887d12b8ebeaf329c044f4974e49607
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177215"
---
# <a name="html-device-information-settings"></a>HTML 设备信息设置
  下表列出了以 HTML 格式呈现时的设备信息设置。  
  
> [!IMPORTANT]  
>  下表列出的带 **(\*)** 的设备信息设置不推荐使用，不应在新应用程序中使用。 有关详细信息，请参阅[SQL Server 2014 中的 SQL Server Reporting Services 中不推荐使用功能](deprecated-features-in-sql-server-reporting-services-ssrs.md)。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|`AccessibleTablix`|指示是否呈现用于屏幕阅读器的其他辅助元数据。 此参数仅适用于包含简单表或具有简单分组的矩阵结构的报表。 默认值是 `false`。 其他辅助元数据可导致所呈现的报表符合电子和信息技术辅助标准（第 508 节）文档的“基于 Web 的 Intranet 和 Internet 信息和应用程序”部分 (1194.22) 中的下列技术标准：<br /><br /> (g) 行标题和列标题应为数据表的标识。<br /><br /> (h) 标记应用来与数据表（该数据表具有行标题或列标题的两个或更多逻辑级别）的数据单元格和标题单元格关联。<br /><br /> (i) 框架应具有便于进行框架标识和导航的文本标题。<br /><br /> 在 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[SPS2010](../includes/sps2010-md.md)]中支持此参数，但在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[SPS2007](../includes/sps2007-md.md)]中则不支持。|  
|**ActionScript(\*)**|指定要在操作事件（如钻取或书签点击）发生时使用的 JavaScript 函数的名称。 如果指定了此参数，则操作事件将触发指定的 JavaScript 函数而不是回发到服务器。|  
|**BookmarkID**|报表中要跳转到的书签 ID。|  
|**DocMap**|指示是显示还是隐藏报表文档结构图。 此参数的默认值是`true`。|  
|`ExpandContent`|指示是否应将报表包含在限制水平大小的表结构中。|  
|**FindString**|要在报表中搜索的文本。 此参数的默认值为空字符串。|  
|**GetImage (\*)**|为 HTML 查看器用户界面获取一个特定的图标。|  
|`HTMLFragment`|指示是否创建一个 HTML 片段以取代完整 HTML 文档。 HTML 片段在 TABLE 语句中包含报表内容，并忽略 HTML 和 BODY 元素。 默认值是 `false`。 使用 SOAP 进行呈现`HTMLFragment`属性设置为`true`创建包含的会话信息可用于正确地请求图像的 Url。 图像必须为报表服务器数据库中的已上载资源。|  
|`ImageConsolidation`|指示是否将呈现的图表、地图、仪表和指示器图像合并为一个大图像。 当报表包含许多数据可视化项目时，图像合并有助于改善客户端浏览器中报表的性能。 默认值是`true`的大多数现代浏览器。|  
|**JavaScript**|指示是否在所呈现报表中支持 JavaScript。 默认值是 `true`。|  
|`LinkTarget`|报表中超链接的目标。 可以通过提供的窗口中，名称如目标窗口或框架`LinkTarget` = *window_name*，或可以确定新窗口中使用的目标`LinkTarget`= _blank。 其他有效的目标名称包括 _self、_parent 和 _top。|  
|**OnlyVisibleStyles(\*)**|指示仅为当前呈现的页生成共享样式。|  
|`OutlookCompat`|指示是否呈现可改善报表在 Outlook 中的外观的额外元数据。 对于其他操作系统，默认值是`false`。|  
|**Parameters**|指示是显示还是隐藏工具栏的参数区域。 如果此参数设置的值为`true`，显示工具栏的参数区域。 此参数的默认值是`true`。|  
|`PrefixId`|与一起使用时`HTMLFragment`，将指定的前缀添加到所有`ID`创建的 HTML 碎片中的属性。|  
|**ReplacementRoot(\*)**|在 ReportViewer 控件之外呈现时预置在报表中的所有钻取、切换和书签链接之前的字符串。 例如，可使用此设置将用户的单击操作重定向到某个自定义页。|  
|**ResourceStreamRoot(\*)**|此字符串预置在所有图像资源的 URL 之前，如用于切换或排序的图像。|  
|**部分**|要呈现的报表的页码。 值为 `0` 指示将呈现报表的所有部分。 默认值是 `1`。|  
|**StreamRoot (\*)**|一个路径，用于添加在由报表服务器返回的 HTML 报表中 IMG 元素的 **src** 属性的值之前。 默认情况下，报表服务器提供此路径。 可以使用此设置为报表中的图像指定根路径（例如，http://\<servername>/resources/companyimages）。|  
|**StyleStream**|指示是否将样式和脚本创建为单独的流，而不是在文档中创建它们。 默认值是 `false`。|  
|`Toolbar`|指示是显示还是隐藏工具栏。 此参数的默认值是`true`。 如果此参数的值是`false`，将忽略所有剩余选项 （文档结构图除外）。 如果您忽略此参数，则自动为支持工具栏的呈现格式显示此工具栏。<br /><br /> 当您使用 URL 访问以呈现报表时，将呈现报表查看器工具栏。 此工具栏不通过 SOAP API 呈现。 但是，`Toolbar`设备信息设置影响的方式显示报表时使用 SOAP`Render`方法。 如果此参数的值是`true`时使用 SOAP 呈现到 HTML，呈现报表中的，仅第一节。 如果值为 `false`，则整个 HTML 报表将呈现为单个 HTML 页。|  
|`UserAgent`|`user-agent`发出请求，可在 HTTP 请求中的浏览器的字符串。|  
|**缩放 (\*)**|整数百分比或字符串常量形式的报表缩放值。 标准字符串值包括 `Page Width` 和 `Whole Page`。 早于 Internet Explorer 5.0 的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 版本和所有非[!INCLUDE[msCoName](../includes/msconame-md.md)] 浏览器忽略此参数。 此参数的默认值是`100`。|  
|**DataVisualizationFitSizing**|指示 tablix 内数据可视化调整大小行为。 这包括图表、仪表和地图。<br /><br /> 可能的值包括 **“近似”** 和 **“精确”**。<br /><br /> 默认值为 **“近似”**。 如果从 **rsreportserver.config** 文件删除该设置，则默认行为为 **“精确”**。<br /><br /> 启用 **“精确”** 可能会影响性能，因为确定精确大小所需的处理时间可能更长。|  
  
## <a name="see-also"></a>请参阅  
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
