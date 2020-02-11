---
title: URL 访问参数引用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b5607f9105ec7197ebc96afc91f189ac19969be8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66098718"
---
# <a name="url-access-parameter-reference"></a>URL 访问参数引用
  可以将下列参数作为 URL 的一部分使用来配置报表的外观。 本节列出了最常用的参数。 参数是区分大小写的，并且如果将其定向到报表服务器，则以参数前缀 rs: 开头，如果定向到 HTML 查看器，则以参数前缀 rc: 开头****。 您也可以指定特定于设备或呈现扩展插件的参数。 有关特定于设备的参数的详细信息，请参阅 [在 URL 中指定设备信息设置](specify-device-information-settings-in-a-url.md)。  
  
> [!IMPORTANT]  
>  非常重要的一点是，URL 包括用于通过 SharePoint 和 `_vti_bin` HTTP 代理路由请求的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 代理语法。 该代理会向 HTTP 请求中添加某一上下文，该上下文是确保为 SharePoint 模式报表服务器正确执行报表所需要的。 有关示例，请参阅 [Access Report Server Items Using URL Access](access-report-server-items-using-url-access.md)。  
>   
>  有关在 URL 中包括报表参数的信息，请参阅 [Pass a Report Parameter Within a URL](pass-a-report-parameter-within-a-url.md)。  
  
## <a name="html-viewer-commands-rc"></a>HTML 查看器命令 (rc:)  
 下表描述了以*rc：* 作为前缀的 URL 访问参数，并使用该参数以 HTML 查看器为目标。  
  
|参数|说明|值|  
|---------------|-----------------|------------|  
|*工具栏*|显示或隐藏工具栏。<br /><br /> ** = `false` ** \*重要提示\* ：对于使用 IP 地址而不是域名的 URL 访问字符串，工具栏不适用于在 SharePoint 站点上承载的\* **报表。|如果此参数的值为 `false`，将忽略所有剩余的选项。 如果您忽略此参数，则自动为支持工具栏的呈现格式显示此工具栏。 此参数的默认值为 `true`。<br /><br /> `true` <br /> `false`|  
|*参数*|显示或隐藏工具栏的参数区域。<br /><br /> `Native`模式示例：<br /><br /> `http://myrshost/reportserver?/Sales&rc:Parameters=Collapsed`<br /><br /> `SharePoint`模式示例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Parameters=Collapsed`|如果将此参数设置为 `true`，将显示工具栏的参数区域。 如果此参数设置为 `false`，则不显示参数区域，用户也不能显示参数区域。 如果此参数设置为 `Collapsed` 值，则不会显示参数区域，但最终用户可以对参数区域进行切换。 此参数的默认值为 `true`。 有效值是：<br /><br /> `true` <br /> `false` <br /> `Collapsed`|  
|*Zoom*|设置报表缩放值，缩放值以整数百分比或字符串常量表示。<br /><br /> `Native`模式示例：<br /><br /> `http://myrshost/reportserver?/Sales&rc:Zoom=Page Width`<br /><br /> `SharePoint`模式示例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Zoom=Page Width`|标准字符串值包括 `Page Width` 和 `Whole Page`。 早于 Internet Explorer 5.0 的 Internet Explorer 版本和所有非[!INCLUDE[msCoName](../includes/msconame-md.md)] 浏览器忽略此参数。 此参数的默认值为 `100`。|  
|*部分*|设置将显示报表中的哪一页。<br /><br /> `Native`模式示例显示报表的第2页：<br /><br /> `http://myrshost/reportserver?/Sales&rc:Section=2`<br /><br /> `SharePoint`模式示例显示报表的第2页：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Section=2`|对于任何设置为大于报表页数的值，都将显示最后一页。 对于任何小于 `0` 的值，都将显示报表的第 1 页。 此参数的默认值为 `1`。|  
|*FindString*|搜索一组特定的文本的报表。<br /><br /> `Native`模式示例：<br /><br /> `http://myrshost/reportserver?/Sales&rc:FindString=Mountain-400`<br /><br /> `SharePoint`模式示例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:FindString=Mountain-400`||  
|*StartFind*|指定要搜索的最后部分。<br /><br /> `Native`模式示例，在产品目录示例报表中搜索文本 "山地-400" 的第一个匹配项，从第一页开始，到第5页结束：<br /><br /> `http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400`|此参数的默认值为报表的最后一页。|  
|*EndFind*|设置要搜索的最后一页的页码。 例如，值 `5` 指示要搜索的最后一页为报表的第 5 页。 请将此参数与 *StartFind* 参数一起使用。 请参阅上述*StartFind*的示例。|默认值为当前页的页码。|  
|*FallbackPage*|设置在搜索或文档结构图选择失败的情况下显示的页码。|默认值为当前页的页码。|  
|*GetImage*|为 HTML 查看器用户界面获取一个特定的图标。||  
|*图标*|获取特定呈现扩展插件的图标。||  
|*表*|指定要应用于 HTML 查看器的样式表。||  
|Device Information Setting|以形式指定设备信息设置`rc:tag=value`，其中*tag*是特定于当前使用的呈现扩展插件的设备信息设置的名称（请参阅*Format*参数的说明）。 例如，可以使用 IMAGE 呈现扩展插件的 OutputFormat 设备信息设置向在 URL 访问字符串中使用以下参数的 JPEG 图像呈现报表：**`...&rs:Format=IMAGE&rc:OutputFormat=JPEG`。 有关所有扩展插件特定的设备信息设置的详细信息，请参阅[呈现扩展插件的设备信息设置 (Reporting Services)](device-information-settings-for-rendering-extensions-reporting-services.md)。||  
  
## <a name="report-server-commands-rs"></a>报表服务器命令 (rs:)  
 下表描述了以*rs：* 作为前缀并用于作为 Report Server 目标的 URL 访问参数。  
  
|参数|说明|  
|---------------|-----------------|  
|*Command*|根据目录项的类型，对其执行操作。 默认值由在 URL 访问字符串中引用的目录项的类型确定。 有效值是：<br /><br /> `ListChildren`并`GetChildren`显示文件夹的内容。 文件夹项显示在一般项导航页内。<br /><br /> `Native`模式示例：<br /><br /> `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`<br /><br /> `SharePoint`模式示例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren`|  
||`Render`呈现指定的报表。<br /><br /> `Native`模式示例：<br /><br /> `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`<br /><br /> `SharePoint`模式示例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`|  
||`GetSharedDatasetDefinition`显示与共享数据集关联的 XML 定义。 共享数据集属性（包括查询、数据集参数、默认值、数据集筛选器以及诸如排序规则和区分大小写之类的数据选项）保存在定义中。 对共享数据集必须具有 **“读取报表定义”** 权限才能使用此值。<br /><br /> `Native`模式示例：<br /><br /> `http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition`|  
||`GetDataSourceContents`将给定共享数据源的属性显示为 XML。 如果您的浏览器支持 XML，且如果您对于该数据源是具有 `Read Contents` 权限的经过身份验证的用户，则将显示数据源定义。<br /><br /> `Native`模式示例：<br /><br /> `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`<br /><br /> `SharePoint`模式示例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`|  
||`GetResourceContents`如果资源与浏览器兼容，则呈现资源并在 HTML 页中显示该资源。 否则，系统会提示您打开文件或资源或将其保存到磁盘。<br /><br /> `Native`模式示例：<br /><br /> `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`<br /><br /> `SharePoint`模式示例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`|  
||`GetComponentDefinition`显示与已发布报表项关联的 XML 定义。 您必须对`Read Contents`已发布的报表项具有权限才能使用此值。|  
|*形式*|指定报表呈现的格式。 常用值包括 `ATOM`、`HTML4.0`、`MHTML`、`IMAGE`、`EXCEL`、`WORD`、`CSV`、`PDF`、`XML`。 默认值是 `HTML4.0`。 有关详细信息，请参阅 [Export a Report Using URL Access](export-a-report-using-url-access.md)。<br /><br /> 例如，若要直接从 `Native` 模式报表服务器获取报表的 PDF 副本。<br /><br /> `http://myrshost/ReportServer?/myreport&rs:Format=PDF`<br /><br /> 例如在模式`SharePoint`中。<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF`|  
|*ParameterLanguage*|提供在与浏览器语言无关的 URL 中传递的参数的语言。 默认值为浏览器语言。 该值可以为区域性值，如 `en-us` 或 `de-de.`。<br /><br /> 例如在 `Native` 模式中，将覆盖浏览器语言并指定区域性值 de-DE。<br /><br /> `http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE`|  
|*快照*|基于报表历史记录快照呈现报表。 有关详细信息，请参阅 [使用 URL 访问呈现报表历史记录快照](render-a-report-history-snapshot-using-url-access.md)。<br /><br /> 例如在 `Native` 模式中，请检索日期为 2003-04-07 且时间戳为 13:40:02 的报表历史记录快照。<br /><br /> `http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02`|  
|*PersistStreams*|呈现单个持久流中的报表。 图像呈现器使用此参数，通过一次传输一块的方式传输呈现的报表。 在 URL 访问字符串中使用此参数后，将相同的 URL 访问字符串用于 *GetNextStream* 参数而非 *PersistStreams* 参数可以获取持久流中的下一个块。 此 URL 命令最终将返回 0 字节流，以指明持久流结束。 默认值是 `false`。|  
|*GetNextStream*|在使用 PersistStreams 参数访问的持久流中获取下一个数据块**。 有关详细信息，请参阅 *PersistStreams*的说明。 默认值是 `false`。|  
|*SessionID*|指定客户端应用程序和报表服务器之间已建立的活动报表会话。 此参数的值设置为会话标识符。<br /><br /> 您可以将会话 ID 指定为 cookie 或 URL 的一部分。 在报表服务器已配置为不使用会话 cookie 时，没有指定会话 ID 的第一个请求将导致具有某一会话 ID 的重定向。 有关报表服务器会话的详细信息，请参阅 [Identifying Execution State](report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)。|  
|*ClearSession*|
  `true` 值指示报表服务器从报表会话中删除报表。 与经过身份验证的用户相关联的所有报表实例都将从报表会话中删除。 （报表实例定义为使用不同报表参数值运行多次的同一报表。）默认值为`false`。|  
|*ResetSession*|
  `true` 值指示报表服务器通过删除报表会话与所有报表快照的关联来重置报表会话。 默认值是 `false`。|  
|*ShowHideToggle*|切换报表部分的显示和隐藏状态。 指定用于表示要切换的部分的正整数。|  
  
## <a name="report-viewer-web-part-commands-rv"></a>报表查看器 Web 部件命令 (rv:)  
 下表介绍了 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 保留的报表参数名称，这些名称用于指向与 SharePoint 集成的报表查看器 Web 部件。 这些参数名称带有 *rv:* 前缀。 报表查看器 Web 部件也接受 *rs:ParameterLanguage* 参数。  
  
|参数|操作|  
|---------------|------------|  
|*工具栏*|控制报表查看器 Web 部件的工具栏显示。 默认值是 `Full`。 值可以是：<br /><br /> 
  `Full`：显示完整的工具栏。<br /><br /> 
  `Navigation`：只显示工具栏中的分页。<br /><br /> 
  `None`：不显示工具栏。<br /><br /> <br /><br /> 例如在 `SharePoint` 模式中，只显示工具栏中的分页。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation`|  
|*HeaderArea*|控制报表查看器 Web 部件的标头显示。 默认值是 `Full`。 值可以是：<br /><br /> 
  `Full`：显示完整的标头。<br /><br /> 
  `BreadCrumbsOnly`：只显示标头中的痕迹导航以告知用户其在应用程序中所处的位置。<br /><br /> 
  `None`：不显示标头。<br /><br /> <br /><br /> 例如在 `SharePoint` 模式中，只显示标头中的痕迹导航。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly`|  
|*DocMapAreaWidth*|控制报表查看器 Web 部件中参数区域的显示宽度（以像素为单位）。 默认值与报表查看器 Web 部件中的默认值一样。 该值必须是非负整数。|  
|*AsyncRender*|控制是否异步呈现报表。 默认值为 `true`，该值指定将异步呈现报表。 该值必须为布尔值 `true` 或 `false`。|  
|*ParamMode*|控制报表查看器 Web 部件的参数提示区域在整页视图中的显示方式。  默认值是 `Full`。 有效值是：<br /><br /> 
  `Full`：显示参数提示区域。<br /><br /> 
  `Collapsed`：折叠参数提示区域。<br /><br /> 
  `Hidden`：隐藏参数提示区域。<br /><br /> 例如在 `SharePoint` 模式中，折叠参数提示区域。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed`|  
|*DocMapMode*|控制报表查看器 Web 部件的文档结构图区域在整页视图中的显示方式。 默认值是 `Full`。 有效值是：<br /><br /> 
  `Full`：显示文档结构图区域。<br /><br /> 
  `Collapsed`：折叠文档结构图区域。<br /><br /> 
  `Hidden`：隐藏文档结构图区域。|  
|*DockToolBar*|控制报表查看器 Web 部件的工具栏是否停靠在顶部或底部。 有效值为 `Top` 和 `Bottom`。 默认值是 `Top`。<br /><br /> <br /><br /> 例如在 `SharePoint` 模式中，将工具栏停靠在底部。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom`|  
|*ToolBarItemsDisplayMode*|控制显示哪些工具栏项。 这是一个按位枚举值。 若要包括某一工具栏项，请将该项的值添加至总值。 例如：如果没有“操作”菜单，请使用 rv:ToolBarItemsDisplayMode=63（或 0x3F），这是 1+2+4+8+16+32 的结果；对于仅限“操作”菜单项，请使用 rv:ToolBarItemsDisplayMode=960（或 0x3C0）。  默认值是 `-1`，这将包括所有工具栏项。 有效值是：<br /><br /> 1 (0x1)：“后退”按钮****<br /><br /> 2 (0x2)：文本搜索控件<br /><br /> 4 (0x4)：页面导航控件<br /><br /> 8 (0x8)：“刷新”按钮****<br /><br /> 16 (0x10)：“缩放”列表框****<br /><br /> 32 (0x20)：“Atom 馈送”按钮****<br /><br /> 64 (0x40)：“操作”中的“打印”菜单选项********<br /><br /> 128 (0x80)：“操作”中的“导出”子菜单********<br /><br /> 256 (0x100)：“操作”中的“使用报表生成器打开”菜单选项********<br /><br /> 512 (0x200)：“操作”中的“订阅”菜单选项********<br /><br /> 1024 (0x400)：“操作”中的“新建数据警报”菜单选项********<br /><br /> 例如，在 " `SharePoint`模式" 下，仅显示 "**后退**" 按钮、文本搜索控件、页面导航控件和 "**刷新**" 按钮。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15`|  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 (SSRS)](url-access-ssrs.md)  
  
  
