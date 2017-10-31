---
title: "添加、 移动或删除文本框 （报表生成器和 SSRS） |Microsoft 文档"
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
ms.assetid: f042cf81-d933-4ac7-9287-c074a46bde98
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 75444343968c9901a24c1a4d431d4d8cfacb1567
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-move-or-delete-a-text-box-report-builder-and-ssrs"></a>添加、移动或删除文本框（报表生成器和 SSRS）
  文本框是 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中最常用的报表项。 您可以向表体添加文本框以显示诸如标题、参数选择、内置字段以及日期之类的信息。  
  
 表或矩阵中的每个单元其实都是一个文本框。 报表中通过表和矩阵显示的所有报表数据几乎都是报表处理器计算报表中每个文本框的内容的结果。 因而，可以用与设置数据区域外其他文本框的格式相同的方式设置单元格式。  
  
 若要向列表数据区域中添加文本框，必须先添加文本框，然后将其拖至列表中。  
  
> [!NOTE]  
>  单击文本框后，便可立即编辑文本框中的文本。 若要选择文本框本身而不是文本框内的文本，请按 ESC。  
  
## <a name="to-add-a-text-box"></a>添加文本框  
  
1.  在“设计”视图的 **“插入”** 选项卡上，单击 **“文本框”**。  
  
2.  在设计图面上，单击并拖动一个框以将其调整到所需文本框大小。  
  
## <a name="to-add-a-text-box-in-a-list"></a>向列表中添加文本框  
  
1.  在报表设计视图的 **“插入”** 选项卡上，单击 **“列表”**。  
  
2.  在设计图面上，单击并拖动一个框以将其调整到所需列表大小。  
  
3.  在 **“插入”** 选项卡上，单击 **“文本框”**。  
  
4.  在设计图面上，在步骤 1 中添加的列表的内部，单击一个框，然后将该框调整为所需文本框大小。   
  
5.  若要确认该文本框已正确嵌套到列表内，请选择该文本框。  
  
    > [!NOTE]  
    >  如果在文本框中单击并处于编辑模式，请按 ESC 以选择文本框。  
  
6.  在“属性”窗格中，验证 **Parent** 属性是否为自动添加到列表数据区域的矩形。  
  
    > [!NOTE]  
    >  如果“属性”窗格不可见，请选中“视图”选项卡上的“属性”。  
  
## <a name="to-move-a-text-box"></a>移动文本框  
  
1.  在报表设计视图中，单击文本框内的任意空白区域以选中文本框。  
  
    > [!NOTE]  
    >  如果在文本框中单击并处于编辑模式，请按 ESC 以选择文本框。  
  
2.  单击文本框控点，然后将该文本框拖至新位置。   
    此外，也可使用箭头键，水平或垂直移动所选文本框。 若要在设计图面上以较小增量移动文本框，请同时按住 Ctrl 键和箭头键。  
  
## <a name="to-delete-a-text-box"></a>删除文本框  
  
1.  在报表设计视图中，右键单击文本框内的任意空白区域以选中该文本框，然后单击“删除”。 此外，也可以单击文本框内的任意空白区域，再按 Delete。  
  
    > [!NOTE]  
    >  如果在文本框中单击并处于编辑模式，请按 ESC 以选择文本框。  
  
## <a name="see-also"></a>另请参阅  
 [文本框 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [表达式 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [键盘快捷方式 &#40;报表生成器 &#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
  
  

