---
title: "以 HTML 格式呈现（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf559b0a-499a-4d74-b520-b382b87e0b17
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: d02ebab15c867e2031ed2001f4f893ea6ee2db6c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="rendering-to-html-report-builder-and-ssrs"></a>以 HTML 格式呈现（报表生成器和 SSRS）
  HTML 呈现扩展插件以 HTML 格式呈现分页报表。 该呈现扩展插件还可以生成完整的 HTML 页面，或生成 HTML 片段以嵌入其他 HTML 页面。 所有 HTML 都是使用 UTF-8 编码生成的。  
  
 在浏览器中查看报表时，包括报表在 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] Web portal 中运行时，HTML 呈现扩展插件都是默认的呈现扩展插件。  
  
 在浏览器中查看报表时，包括报表在 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] Web portal 中运行时，HTML 呈现扩展插件都是默认的呈现扩展插件。 HTML 呈现扩展插件可以将 HTML 呈现为片段或完整的 HTML 文档。 如果 HTML 为片断形式，则会删除 HTML 文档的 **HEAD**、 **HTML**和 **BODY** 标记。 只有 **BODY** 标记的内容才会呈现。 这在将此 HTML 片段嵌入其他应用程序生成的 HTML 时颇为有用。  
  
 在某些情况下，以 HTML 格式呈现报表时，报表参数可用于发起脚本注入攻击。 有关保护报表的详细信息，请参阅 [保护报表和资源](../../reporting-services/security/secure-reports-and-resources.md)。  
  
 有关浏览器的详细信息，请参阅 [Reporting Services 和 Power View 的浏览器支持](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RenderingMHTML"></a> 以 MHTML 格式呈现  
 HTML 呈现扩展插件还可以将报表呈现为 MHTML 格式（聚合 HTML 文档的 MIME 封装）。 MHTML 扩展了 HTML 以实现在 HTML 文档中嵌入图像等编码对象。 使用 MHTML 呈现扩展插件后，可将图像、文档或其他二进制文件等资源作为报表 HTML 内的 MIME 结构嵌入单个文件中。 MHTML 报表也可用于嵌入到电子邮件中，因为所有资源都包含在报表中。 虽然实际上呈现 MHTML 的是 HTML 呈现扩展插件，但此功能也可称为 MHTML 呈现扩展插件。  
  
  
##  <a name="BrowserSupport"></a> 浏览器支持  
 此呈现扩展插件支持以下浏览器版本：  
  
-   Internet Explorer 5.5 和更高版本  
  
-   FireFox 1.5 和更高版本  
  
-   Safari 3.0 和更高版本  
  
 出于跨浏览器的考虑，呈现的报表可能因浏览器的不同而稍有差别。 例如，文本框包含名为 WritingMode 的属性。 Firefox 不支持此属性。  
  
  
##  <a name="HTMLSpecificRenderingRules"></a> 特定于 HTML 的呈现规则  
 呈现时将应用下列特定于 HTML 的规则：  
  
-   呈现器生成一个 HTML 表结构，以包含每个 **ReportItems** 集合（如果存在多个集合）中的所有项。  
  
-   表结构中的每一项都占用一个单元。  
  
-   空单元会尽可能折叠在一起以减少 HTML 的大小。  
  
-   会向上边缘添加一行空单元并向左边缘添加一列空单元以提高浏览器呈现表的速度。  
  
-   对于不包含任何项的表行或表列，即项之间的空白，以固定宽度和高度显示。  
  
-   其他所有行和列均允许根据每个报表项的尺寸增长。  
  
-   所有坐标和报表项尺寸的单位均转换为毫米。 其他所有尺寸（包括样式属性）均保留其原始单位。 小于 0.2mm 的尺寸差和位置差均视为 0mm。  
  
  
##  <a name="Interactivity"></a> 交互  
 HTML 支持一些交互元素。 下面是对一些特定行为的说明。  
  
### <a name="show-and-hide"></a>显示和隐藏  
 可以切换可见性的报表项呈现时会带有一个 +/- 切换图像，并且该报表项是可以单击的。 单击该项后，将回调到服务器以重新呈现该项在更改了显示或隐藏状态后的输出。  
  
### <a name="document-map"></a>文档结构图  
 文档结构图标签将呈现出来，并可通过在查看器控件中使用文档结构图进行定位。 如果数据区域表头已省略，标签将呈现在第一个子单元上。 如果不存在相应的子单元，标签将呈现在其标记处前面的子单元上。  
  
### <a name="bookmarks"></a>书签  
 书签链接以超链接形式呈现和显示。 标签目标将呈现出来并可通过单击书签链接进行定位。 单击书签链接后，报表将跳转到目标书签标签的首次出现处，并且如有可能，浏览器将滚动以便书签链接处于窗口顶部。 HTML 定位点 (\<a>) 标记用于标记书签目标。  
  
### <a name="interactive-sorting"></a>交互式排序  
 如果已为某一文本框定义了用户排序，则 HTML 呈现扩展插件将在该文本框内呈现排序图标，呈现位置为文本框内容的右侧。 如果报表包含任何已定义用户排序的文本框，则单击相应排序图标后将呈现导致回发到服务器的 JavaScript。  
  
### <a name="hyperlinks-and-drillthrough"></a>超链接和钻取  
 报表项上的超链接和钻取链接都呈现为超链接，呈现方法为在这些链接所定义的项周围放置 HTML 定位点 (\<a>) 标记。  
  
### <a name="search"></a>搜索  
 搜索功能允许用户在报表内搜索文本字符串。  
  
 其他搜索和查找功能由 ReportViewer Web 窗体控件提供。  
  
  
##  <a name="DeviceInfo"></a> 设备信息设置  
 您可以通过更改设备信息设置来更改此呈现器的某些默认设置（包括以哪个模式呈现）。 有关详细信息，请参阅 [HTML Device Information Settings](../../reporting-services/html-device-information-settings.md)。  
  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [呈现报表项（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
