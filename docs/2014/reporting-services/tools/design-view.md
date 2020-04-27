---
title: “设计”视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.layoutview.f1
helpviewer_keywords:
- Layout View dialog box
ms.assetid: 6fa378aa-442f-4d2f-beab-02a0fb5cd3ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63ac5bf29ca441a18be4bc5e46448475b56104bc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100301"
---
# <a name="design-view"></a>设计视图
  使用“设计”视图可以排列报表中的报表项。 设计视图有时称为设计图面或布局视图。  
  
## <a name="report-design-surface"></a>报表设计图面  
 设计图面由三个部分组成：表体、页眉和页脚。 使用工具箱可以选择要放置在这三个部分的任一部分中的项。 使用“报表数据”窗格可以查看图像、参数、数据源以及数据集（包括数据集查询和字段列表）。 将报表项添加到设计图面后，请将数据集字段从 **“报表数据”** 窗格拖至数据区域（如表、矩阵或列表）。 报表设计图面上的每一项都包含属性，这些属性可以通过使用属性对话框或“属性”窗格进行管理。  
  
## <a name="toolbox"></a>工具箱  
 工具箱列出了可用于报表的数据区域和其他报表项。 若要从工具箱添加报表项，请双击该报表项或将其拖至设计图面。 然后使用对象控点可以更改报表项的形状和大小。  
  
## <a name="report-data-pane"></a>“报表数据”窗格  
 若要查看“报表数据”窗格，请在 **“视图”** 菜单上单击 **“报表数据”**。 使用此窗格可以定义参数、图像、数据源以及数据集，还可以引用内置字段（如 ReportName）。 若要添加新项，请单击 **“新建”** 菜单，然后选择一项。 若要将计算字段添加到现有数据集，请单击 **“数据集”**，然后在 **“数据集属性”** 对话框中，选择 **“字段”**。 选择一项，然后单击 **“编辑”** 打开 **“属性”** 对话框。 还可以在“报表数据”窗格中，右键单击项以添加项或更新项的属性。  
  
 将项从“报表数据”窗格拖至设计图面上的数据区域和文本框可将数据和图像添加到报表中。  
  
 有关详细信息，请参阅 [Report Data Pane](../report-data/report-data-pane.md)。  
  
## <a name="grouping-pane"></a>“分组”窗格  
 使用组可以将报表数据组织成可视层次结构，也可以计算总计。 使用“分组”窗格可以查看为表、矩阵或列表数据区域定义的组。 默认情况下，“分组”窗格将所选数据区域的所有组显示为一个平展列表。 对图表和仪表数据区域禁用“分组”窗格。  
  
 若要查看各组彼此之间的关系，请将“分组”窗格切换为高级模式。 此模式显示了组成员的层次结构，并以可视方式显示了与每个组对应的数据区域中的单元。  
  
 有关详细信息，请参阅 [Grouping Pane](grouping-pane.md)。  
  
## <a name="page-header-and-page-footer"></a>页眉和页脚  
 页眉和页脚分别位于每一页的顶部和底部。 页眉和页脚可以包含静态文本、图像、线条、矩形、边框、背景色和背景图像。 若要将报表项添加到页眉和页脚，请右键单击设计图面，然后选择“页眉”或“页脚”。 页眉和页脚部分将显示在设计图面上。  
  
## <a name="properties-pane"></a>“属性”窗格  
 使用“属性”窗格可以查看设计图面上当前所选的报表项或“分组”窗格中的当前所选组。 另外，也可以右键单击所选报表项或组，然后单击“属性”打开报表项或组的相应“属性”对话框********。  
  
## <a name="see-also"></a>另请参阅  
 [页眉和页脚 &#40;报表生成器和 SSRS&#41;](../report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [报表设计提示（报表生成器和 SSRS）](../report-design/report-design-tips-report-builder-and-ssrs.md)  
  
  
