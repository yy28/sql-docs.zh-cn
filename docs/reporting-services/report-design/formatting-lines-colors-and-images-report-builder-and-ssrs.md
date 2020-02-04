---
title: 设置线条、颜色和图像的格式（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.textboxproperties.border.f1
- "10502"
- "10094"
- sql13.rtp.rptdesigner.shared.borderdv.f1
- sql13.rtp.rptdesigner.reportbody.border.f1
- "10063"
- sql13.rtp.rptdesigner.pictureproperties.border.f1
- sql13.rtp.rptdesigner.rectangleproperties.border.f1
- "10055"
- "10126"
- "10066"
- sql13.rtp.rptdesigner.subreportproperties.border.f1
ms.assetid: 0f5f0d2a-9537-4152-b441-b40d7f04cf4c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3bc6e9b634ce9872b069381d58ed2dc89a0dc1d4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65576007"
---
# <a name="formatting-lines-colors-and-images-report-builder-and-ssrs"></a>设置线条、颜色和图像的格式（报表生成器和 SSRS）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可以设置线条、颜色、数据区域、图像和其他报表项的格式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="borders-lines-and-gridlines"></a>边框、线条和网格线  
 使用边框、线条和网格线可以直观地将页中的项关联在一起，并有助于报表读者轻松读取报表的内容。 通过使用预定义的边框样式，您可以快速地在文本框、文本框组或图像周围添加边框。 此外，还可以更改边框、线条和网格线的样式、宽度和颜色。 边框通常添加在整个选定项的周围，或沿着项边缘的边框添加，例如，沿着文本框底部的边框。  
  
 若要设置文本框、报表布局或图像周围的边框和网格线的格式，请使用报表项的 **“属性”** 对话框中的 **“边框”** 选项卡。 例如，如果要在图像周围添加边框，请右键单击该图像然后在 **“图像属性”** 对话框中，单击 **“边框”** 。  
  
 除了标准边框外，还可以对图表应用其他边框。 有关详细信息，请参阅[向图表添加边框（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)。  
  
 也可将边框添加到报表自身中。 有关详细信息，请参阅 [向报表添加边框（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)的详细信息。  
  
## <a name="applying-background-colors"></a>应用背景色  
 可以将纯色添加到整个报表或报表内文本框的背景中，也可以添加到数据区域内的单元或单元组。 默认情况下，背景色为白色；不过，您可以从报表项中 **“属性”** 对话框的 **“填充”** 选项卡中选择颜色。 例如，如果要更改文本框的背景色，请右键单击该文本框，然后选择 **“文本框属性”** 。 单击 **“填充”** ，然后选择需要的颜色。 在此对话框中，可以为所选项选择背景色，也可以添加背景中显示的图像。  
  
 使用图表时，还可以指定背景色的渐变样式和图案样式。 有关详细信息，请参阅[设置图表格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="using-images-as-formatting"></a>使用图像作为格式  
 可以向数据区域添加包含图像的字段。 如果使用图像字段，则运行报表时将在报表中显示图像。  
  
 还可以将图像（如徽标）添加到报表的背景中，或添加到矩形、文本框、表、矩阵或某些图表部件中，或添加到表体和页部分。 有关详细信息，请参阅[图像（报表生成器和 SSRS）](../../reporting-services/report-design/images-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [设置文本和占位符的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [设置数字和日期格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [设置文本框中文本的格式（报表生成器和 SSRS）](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)   
 [“填充”对话框（报表生成器和 SSRS）](https://msdn.microsoft.com/library/93a91d02-d558-4a0e-8d17-3fdf21e208d3)  
  
  
