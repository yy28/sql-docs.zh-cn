---
title: 导出到 PDF 文件（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f22497b7-f6c1-4c7b-b831-8c731e26ae37
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b3eb41d807a1b4678882c791a7bdeb7693de7b08
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107914"
---
# <a name="exporting-to-a-pdf-file-report-builder-and-ssrs"></a>导出到 PDF 文件（报表生成器和 SSRS）
  PDF 呈现扩展插件可将报表呈现为特定格式的文件，以便在 Adobe Acrobat 和其他支持 PDF 1.3 的第三方 PDF 查看器中打开。 尽管 PDF 1.3 与 Adobe Acrobat 4.0 及更高版本兼容，但 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持 Adobe Acrobat 6 或更高版本。 呈现扩展插件不需要使用 Adobe 软件呈现报表。 不过，该插件需要使用 PDF 查看器（例如 Adobe Acrobat）才可查看或打印 PDF 格式的报表。  
  
 PDF 呈现扩展插件支持 ANSI 字符，并且可以从日语、朝鲜语、繁体中文、简体中文、西里尔语、希伯来语和阿拉伯语转换 Unicode 字符，但存在一些限制。 有关限制的详细信息，请参阅[导出报表 &#40;报表生成器和 SSRS&#41;](export-reports-report-builder-and-ssrs.md)。  
  
 PDF 呈现器是一个物理页呈现器，因此其分页行为与诸如 HTML 和 Excel 等其他呈现器不同。 本主题提供了特定于 PDF 呈现器的信息并说明了呈现规则的例外情况。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="font-embedding"></a><a name="FontRequirements"></a> 嵌入字体  
 如有可能，PDF 呈现扩展插件会在 PDF 文件中嵌入显示报表所需的每个字体的子集。 因此报表服务器上必须安装有报表中使用的字体。 当报表服务器以 PDF 格式生成报表时，它将使用报表引用的字体中所存储的信息在 PDF 文件内创建字符映射。 如果报表服务器上未安装所引用的字体，生成的 PDF 文件可能不会包含正确的映射，因而在查看该 PDF 文件时可能不会正常显示。  
  
 满足以下条件时，将在 PDF 文件中嵌入字体：  
  
-   字体作者授予了嵌入字体的权限。 安装的字体包含一个属性，该属性指示字体作者是否打算允许在文档中嵌入字体。 如果该属性值为 EMBED_NOEMBEDDING，将不会在 PDF 文件中嵌入字体。 有关详细信息，请参阅 msdn.microsoft.com 上的“TTGetEmbeddingType”。  
  
-   该字体为 TrueType。  
  
-   字体由报表中的可见项引用。 如果字体由 Hidden 属性设置为 True 的项引用，则显示呈现的数据不需要字体，所以不会在文件中包含字体。 只有显示所呈现的报表数据需要字体时，才会嵌入字体。  
  
 如果某个字体满足上述所有条件，将在 PDF 文件中嵌入该字体。 如果不满足上述一个或多个条件，将不会在 PDF 文件中嵌入该字体。  
  
> [!NOTE]  
>  即使条件满足，还会有一种 PDF 文件未嵌入字体的情况。 如果所用字体包含在 PDF 规范（常称作 standard type 1 字体或十四个基础字体）中，则对于 ANSI 内容，将不嵌入字体。  
  
  
  
### <a name="fonts-on-the-client-computer"></a>客户端计算机上的字体  
 如果在 PDF 文件中嵌入了字体，则用于查看报表的计算机（客户端计算机）不必安装字体即可正确显示报表。  
  
 如果 PDF 文件中没有嵌入字体，则客户端计算机必须安装正确的字体才能正确显示报表。 如果客户端计算机上没有安装字体，则对于不支持的字符，PDF 文件将显示问号字符 (?)。  
  
### <a name="verifying-fonts-in-a-pdf-file"></a>验证 PDF 文件中的字体  
 PDF 输出差异通常在报表中使用不支持非拉丁字符的字体并随后将非拉丁字符添加到报表时发生。 应在报表服务器和客户端计算机上测试 PDF 呈现输出，以验证报表是否正常呈现。  
  
 请勿依赖在预览模式下查看报表或导出到 HTML，这是因为报表会因图形设计界面或 Microsoft Internet Explorer 分别执行的自动字体替换而正确显示。 如果服务器上缺少 Unicode 标志符号，您可能会看到字符被替换为问号 (?)。 如果客户端上缺少字体，你可能会看到字符被替换为方框 (□)。  
  
 嵌入 PDF 文件的字体包含在“字体”属性中，该属性随文件一起作为元数据保存。  
  
##  <a name="metadata"></a><a name="Metadata"></a>新元  
 除了报表布局外，PDF 呈现扩展插件会将以下元数据写入 PDF 文档信息字典。  
  
|PDF 属性|创建自|  
|------------------|------------------|  
|`Title`|`Name` RDL 元素的 `Report` 属性。|  
|`Author`|`Author` RDL 元素。|  
|`Subject`|`Description` RDL 元素。|  
|`Creator`|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 产品的名称和版本。|  
|`Producer`|呈现扩展插件的名称和版本。|  
|`CreationDate`|报表执行时间，以 PDF `datetime` 格式表示。|  
  
  
  
##  <a name="interactivity"></a><a name="Interactivity"></a>互动  
 PDF 支持一些交互元素。 下面是对一些特定行为的说明。  
  
### <a name="show-and-hide"></a>显示和隐藏  
 PDF 不支持动态显示和隐藏元素。 呈现 PDF 文档是为了与报表中任意项的当前状态相匹配。 例如，如果在报表初次运行时显示了某项，则会呈现该项。 如果可切换的图像在导出报表时隐藏，则不会呈现这些图像。  
  
### <a name="document-map"></a>文档结构图  
 如果报表中存在任何文档结构图标签，则会将文档大纲添加到 PDF 文件。 每个文档结构图标签在文档大纲中显示为一个条目，显示顺序与其在报表中的显示顺序相同。 在 Acrobat 中，仅当目标书签所在的页呈现出来时，才会将该标签添加到文档大纲中。  
  
 如果仅呈现单个页，则不添加文档大纲。 文档结构图是分层排列的，以反映报表中的嵌套级别。 文档大纲在 Acrobat 中的 "书签" 选项卡下是可访问的。单击文档大纲内的条目将导致文档进入带有书签的位置。  
  
### <a name="bookmarks"></a>书签  
 PDF 呈现不支持书签。  
  
### <a name="drillthrough-links"></a>钻取链接  
 在 PDF 呈现中不支持钻取链接。 钻取链接不呈现为可单击链接，并且钻取报表不能连接到钻取的目标。  
  
### <a name="hyperlinks"></a>超链接  
 报表中的超链接在 PDF 文件中呈现为可单击的链接。 单击超链接时，Acrobat 将打开默认的客户端浏览器并导航到超链接 URL。  
  
  
  
##  <a name="compression"></a><a name="Compression"></a>折叠  
 图像压缩基于图像的原始文件类型。 默认情况下，PDF 呈现扩展插件会压缩 PDF 文件。  
  
 为了尽可能保留 PDF 文件中所包含图像的任何压缩状态，JPEG 图像存储为 JPEG，所有其他图像类型都存储为 BMP。  
  
> [!NOTE]  
>  PDF 文件不支持嵌入 PNG 图像。  
  
  
  
##  <a name="device-information-settings"></a><a name="DeviceInfo"></a>设备信息设置  
 您可以通过更改设备信息设置来更改此呈现器的某些默认设置。 有关详细信息，请参阅 [PDF Device Information Settings](../pdf-device-information-settings.md)。  
  
  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services &#40;报表生成器和 SSRS 中的分页&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为 &#40;报表生成器和 SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能 &#40;报表生成器和 SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [&#40;报表生成器和 SSRS 呈现报表项&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
