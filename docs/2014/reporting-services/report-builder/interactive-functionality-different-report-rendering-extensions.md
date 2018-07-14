---
title: 不同报表呈现扩展插件 （报表生成器和 SSRS） 的交互功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f0bd1c4c-e8b5-467f-b5a1-541f19c7e3e2
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a61442deaf2ca75bd3fb85f5eb8c83f6f58c4fee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238487"
---
# <a name="interactive-functionality-for-different-report-rendering-extensions-report-builder-and-ssrs"></a>不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了可用于在运行时处理报表的交互式报表功能。 并非所有的报表呈现格式都支持整套交互功能。 您可以通过下表了解每项交互功能在处理特定格式时的工作原理。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="interactive-features-in-different-output-formats"></a>不同输出格式中的交互功能  
 呈现为 XML、CSV 或图像格式的报表不支持交互功能。  
  
 在报表管理器、SharePoint Web 部件或浏览器中查看的报表以 HTML 形式呈现。 只有 HTML 和 Windows 窗体这两种报表输出格式才完全支持所有交互功能。 其他 HTML 格式（如 MHTML）也支持许多交互功能。 下表注明了 MHTML 不支持的交互功能。  
  
### <a name="document-maps"></a>文档结构图  
  
|导出选项|支持信息|  
|-------------------|-------------------------|  
|预览/报表查看器，HTML|交互式文档结构图提供了一个包含层次结构链接的导航窗格，可使用此窗格导航到报表的不同区域。|  
|PDF|PDF 将文档结构图呈现为“书签”窗格。 文档结构图中的所有项都将在该窗格中依次向下列出。 它包含一个链接层次结构。 如果指定了页面范围，则只有那些已呈现的书签才会存在于该层次结构中。|  
|“导出”|Excel 将文档结构图呈现为工作簿中的第一个工作表。 它包含一个链接层次结构。 如果单击文档结构图中的链接，则会打开各自工作表中的相应目标单元格。|  
|Word|Word 将文档结构图呈现为目录标签。|  
|其他（例如，TIFF、XML 和 CSV）|无法以 MHTML、XML、CSV 或图像格式实现。|  
  
### <a name="drillthrough-links-to-other-reports"></a>指向其他报表的钻取链接  
  
|导出选项|支持信息|  
|-------------------|-------------------------|  
|预览/报表查看器，HTML|用户单击报表中的数据值便可查看其他报表中的相关数据。|  
|PDF|钻取链接在 PDF 中不可用。 对于链接到其他页的 PDF 报表，请考虑使用超链接。|  
|“导出”|钻取链接以 Excel 呈现。<br /><br /> 链接转换为指向钻取链接所引用报表的超链接。 单击链接时便会在浏览器窗口中打开一个报表。|  
|Word|钻取链接以 Word 呈现。<br /><br /> 链接转换为指向钻取链接所引用报表的超链接。 单击链接时便会在浏览器窗口中打开一个报表。|  
|其他|无法以 XML、CSV 或图像格式实现。|  
  
### <a name="toggle-items-within-a-report"></a>报表中的切换项  
  
|导出选项|支持信息|  
|-------------------|-------------------------|  
|预览/报表查看器，HTML|用户单击展开和折叠图标便可查看报表的区域。|  
|PDF|报表服务器将当前处于显示或隐藏状态的报表导出为 PDF。 不支持交互式切换|  
|“导出”|可切换的钻取链接和项在 Excel 中呈现为可折叠大纲。 您可以在 Excel 中展开和折叠报表的区域。 有关 Excel 强制限制的详细信息，请参阅[导出到 Microsoft Excel（报表生成器和 SSRS）](exporting-to-microsoft-excel-report-builder-and-ssrs.md)。|  
|Word|报表服务器将当前处于显示或隐藏状态的报表导出为 PDF。 不支持交互式切换|  
|其他|无法以 MHTML、XML 或 CSV 格式实现。 如果导出为图像格式，则报表服务器会将当前处于显示或隐藏状态的报表导出为 PDF。 不支持交互式切换。|  
  
### <a name="interactive-sorting"></a>交互式排序  
  
|导出选项|支持信息|  
|-------------------|-------------------------|  
|预览/报表查看器，HTML|对于表格报表，用户单击列中的排序箭头便可更改数据的排序方式。|  
|PDF|无法在 PDF 中实现。|  
|“导出”|无法在 Excel 中实现。|  
|Word|无法在 Word 中实现。|  
|其他|无法以 MHTML、XML、CSV 或图像格式实现。|  
  
### <a name="hyperlinks-to-external-web-content-or-images"></a>指向外部 Web 内容或图像的超链接  
  
|导出选项|支持信息|  
|-------------------|-------------------------|  
|预览/报表查看器，HTML|用户单击这些链接便可在新的浏览器窗口中打开外部网页。|  
|PDF|超链接通过 PDF 呈现扩展插件呈现。 用户单击某个超链接时，将在浏览器中打开该链接指向的页。|  
|Excel|超链接以 Excel 呈现。|  
|Word|超链接以 Word 呈现。|  
|其他|超链接无法以 MHTML、XML、CSV 或图像格式实现。<br /><br /> 对于 MHTML 和图像格式，外部图像呈现为静态图片。|  
  
### <a name="bookmark-or-anchor"></a>书签或定位点  
  
|导出选项|支持信息|  
|-------------------|-------------------------|  
|预览/报表查看器，HTML|用户单击链接便可导航到同一报表的其他区域。|  
|PDF|无法在 PDF 中实现。|  
|“导出”|书签在 Excel 中呈现。<br /><br /> 书签转换为指向报表项的名称的超链接。|  
|Word|书签在 Word 中呈现。<br /><br /> 书签转换为指向有书签的报表项的超链接。 导出报表时，仅可转换 40 个字符的书签名称或定位点名称，这可能导致书签名称或定位点名称重复。 空格转换为下划线 (_)。|  
|其他|无法以 XML、CSV 或图像格式实现。|  
  
### <a name="prompted-parameters-obtained-at-run-time"></a>运行时获取的提示参数  
  
|导出选项|支持信息|  
|-------------------|-------------------------|  
|预览/报表查看器，HTML|参数输入区域在报表的顶部显示。 此区域是用于在浏览器中显示报表的 HTML 查看器的一部分。|  
|PDF|报表服务器使用当前对报表有效的参数值将报表导出为 PDF。|  
|“导出”|报表服务器使用当前对报表有效的参数值将报表导出为 Excel。|  
|Word|报表服务器使用当前对报表有效的参数值将报表导出为 Word。|  
|其他|报表服务器使用当前对报表有效的参数值将报表导出为其他格式。|  
  
### <a name="filters-applied-at-run-time"></a>在运行时应用的筛选器  
  
|导出选项|支持信息|  
|-------------------|-------------------------|  
|预览/报表查看器，HTML|在运行时向用户显示经过筛选的数据。|  
|PDF|报表服务器使用当前报表中的已筛选数据将报表导出为 PDF。|  
|“导出”|报表服务器使用当前报表中的已筛选数据将报表导出为 Excel。|  
|Word|报表服务器使用当前报表中的已筛选数据将报表导出为 Word。|  
|其他|报表服务器使用当前报表中的已筛选数据将报表导出为其他格式。|  
  
## <a name="see-also"></a>请参阅  
 [导出报表&#40;报表生成器和 SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [交互式排序、文档结构图和链接（报表生成器和 SSRS）](../report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](../report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [图表&#40;报表生成器和 SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
  
