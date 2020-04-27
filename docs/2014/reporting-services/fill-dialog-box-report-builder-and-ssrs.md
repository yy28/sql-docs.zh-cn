---
title: "\"填充\" 对话框（报表生成器和 SSRS） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportbody.fill.f1
- "10065"
- "10501"
- sql12.rtp.rptdesigner.shared.filldv.f1
- sql12.rtp.rptdesigner.rectangleproperties.fill.f1
- "10064"
- sql12.rtp.rptdesigner.textboxproperties.fill.f1
- "10124"
ms.assetid: 93a91d02-d558-4a0e-8d17-3fdf21e208d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86f54b00e530e70d1952461ce7b98b9238e4c3f3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109159"
---
# <a name="fill-dialog-box-report-builder-and-ssrs"></a>“填充”对话框（报表生成器和 SSRS）
  在 **“填充”** 选项卡上，您可以为数据区域或文本框中的单个或多个单元的背景指定颜色选项。  
  
## <a name="options"></a>选项  
 **填充颜色**  
 单击此颜色按钮可为矩形选择填充颜色。 单击“表达式”_(fx)_ 按钮可编辑表达式，此表达式可以是 RGB 颜色的十六进制值，也可以是“表达式”对话框中提供的预定义的颜色名称之一。******** 若要查看预定义的颜色的列表，请在 **“项”** 窗格中选择 **Web**。 可在表达式文本窗格中键入 **“标题”** 窗格中列出的颜色名称。 键入颜色名称时请勿使用等号 (=) 或引号 ("")。  
  
 **选择图像源**  
 指示图像的存储位置，以便在呈现报表时报表处理器能够显示它。  
  
-   **外部** 如果您希望此图像继续作为文件存在于报表服务器或 Web 服务器上，请选择此选项。  
  
-   **嵌入** 如果您希望将此图像嵌入到报表中，请选择此选项。  
  
-   **数据库** 如果您希望包括表示您要包含在报表中的图像的数据库字段名称，请选择此选项。  
  
 **使用此图像**  
 选择“嵌入”**** 或“外部”**** 选项时，便会出现此选项。  
  
 如果您要嵌入相应图像，请从下拉列表中选择您要添加到报表中的图片。 单击“导入”可将图像添加到下拉列表中。**** 如果向“数据”窗格添加了一张图像，则可以通过如下方法选择此图像：选择“嵌入”，然后从下拉列表中选择此图像。********  
  
 如果您选择 **“外部”** 选项，请键入相应图像的 URL。 对于发布到配置为纯模式的 Report Server 的报表，请使用完整路径或相对路径（例如，http://*\<servername>*/images/image1.jpg）。 对于发布到在 SharePoint 集成模式下配置的 Report Server 的报表，请使用完全限定的 URL （例如，http://*\<服务器名称>\</site>*/Documents/images/image1.jpg）。  
  
 **导入**  
 此选项在选择“嵌入”后可用。**** 单击此选项可以向“使用此图像”**** 下拉列表中添加图像。  
  
 **使用此字段**  
 此选项在选择“数据库”后可用。**** 请选择字段名称。  
  
 **使用此 MIME 类型**  
 选择数据库中包含的图片的适当格式（例如，.bmp、.jpeg、.gif、.png 或 .x-png）。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;报表生成器和 SSRS 的格式设置报表项&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [设置文本和占位符的格式 &#40;报表生成器和 SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [图像（报表生成器和 SSRS）](report-design/images-report-builder-and-ssrs.md)  
  
  
