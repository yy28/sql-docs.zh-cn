---
title: "将 HTML 添加到报表 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 17889109d30d41405b0fa13d694e29930b82a292
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>向报表添加 HTML（报表生成器和 SSRS）
  可以使用占位符从数据集中的字段导入 HTML 以在报表中使用。 默认情况下，占位符表示纯文本，因此需要将占位符的标记类型改为 HTML。 有关详细信息，请参阅[将 HTML 导入报表（报表生成器和 SSRS）](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>将 HTML 从数据集中的字段添加到文本框中  
  
1.  在 **“插入”** 选项卡上，单击 **“列表”**。 单击设计图面，然后拖动鼠标根据所需大小创建一个文本框。  
  
     此时将打开 **“数据集属性”** 对话框。 可以使用共享数据集或嵌入在报表中的数据集。 有关详细信息，请单击[“数据集属性”对话框 ->“查询”（报表生成器）](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md)或[“数据集属性”对话框，“查询”](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f)。  
  
2.  在 **“插入”** 选项卡上，单击 **“文本框”**。 在列表中单击，然后拖动鼠标根据所需大小创建一个文本框。  
  
3.  将数据集中的 HTML 字段拖到文本框中。 此时将为您的字段创建一个占位符。  
  
4.  右键单击该占位符，然后单击“占位符属性”。  
  
5.  在 **“常规”** 选项卡中，确保 **“值”** 框中包含要对您在步骤 3 中所放置字段进行比较的表达式。  
  
6.  单击“HTML - 将 HTML 标记解释为样式”。 这会使字段被视为 HTML。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [格式设置数字和日期 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [格式设置线条、 颜色和图像 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [占位符属性对话框，常规 &#40;报表生成器和 SSRS &#41;](http://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
