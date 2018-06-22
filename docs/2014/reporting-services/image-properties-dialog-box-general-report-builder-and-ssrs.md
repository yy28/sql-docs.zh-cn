---
title: 图像属性对话框，常规 （报表生成器和 SSRS） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
caps.latest.revision: 12
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 26c0378caeca7fd904cd793bc483dd28a464a5d2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014247"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>“图像属性”对话框 -&gt;“常规”（报表生成器和 SSRS）
  在 **“图像属性”** 对话框中选择 **“常规”** 可添加图片、更改图像的默认名称，还可以添加工具提示文本。  
  
## <a name="options"></a>“常规”  
 **名称**  
 为相应项键入一个名称。 该名称在报表中必须是唯一的。 默认情况下会分配一个常规名称，例如 Image1 或 Image2。  
  
 **工具提示**  
 键入文本或计算结果为工具提示的表达式。 单击“表达式”(*fx*) 按钮可编辑表达式。 当用户将鼠标指针停在 HTML 报表中该项的上方时，便会显示此 **“工具提示”** 。  
  
 **选择图像源**  
 指示图像的存储位置，以便在呈现报表时报表处理器知道从何处获取图像。  
  
-   **外部** 如果您希望此图像继续作为文件存在于报表服务器或 Web 服务器上，请选择此选项。  
  
-   **嵌入** 如果您希望将此图像嵌入到报表中，请选择此选项。  
  
-   **数据库** 如果您希望包括表示您要包含在报表中的图像的数据库字段名称，请选择此选项。  
  
 **使用此图像**  
 选择“嵌入”或“外部”选项时，便会出现此选项。  
  
 如果要嵌入图像，请从下拉列表中选择要添加到报表中的图像。 单击“导入”按钮可将图像添加到下拉列表中。  
  
 如果您选择 **“外部”** 选项，请键入相应图像的 URL。 对于发布到配置为本机模式的报表服务器的报表，请使用完整路径或相对路径。 例如，http://\<服务器名 > / images/image1.jpg。 对于发布到配置为 SharePoint 集成模式的报表服务器的报表，请使用完全限定的 URL。 例如，http://\<*SharePointservername*>/\<*站点*> / Documents/images/image1.jpg。  
  
 **导入**  
 单击此选项可以向“使用此图像”下拉列表中添加图像。  
  
 **使用此字段**  
 如果选择“数据库”选项，便会出现此选项。 请选择字段名称。  
  
 **使用此 MIME 类型**  
 选择数据库中包含的图像的适当格式（例如 .bmp、.jpeg、.gif、.png 和 .x-png）。  
  
## <a name="see-also"></a>请参阅  
 [表达式示例（报表生成器和 SSRS）](report-design/expression-examples-report-builder-and-ssrs.md)   
 [映像&#40;报表生成器和 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [用于对话框、 窗格和向导的报表生成器帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  