---
title: 向报表添加书签（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f130562e-5673-40e3-8e01-de7227a21d41
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c0303996c4db22d05a288ce055201a343e330778
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290243"
---
# <a name="add-a-bookmark-to-a-report-report-builder-and-ssrs"></a>向报表添加书签（报表生成器和 SSRS）
  若要在报表中提供自定义目录或自定义内部导航链接，可以向报表中添加书签或书签链接。 通常情况下，如果要引导用户到报表中的某一位置，例如表、图表以及表或矩阵中显示的唯一组值，可以向该位置添加书签。 可以创建用作书签的字符串；或者，对于组而言，可以将书签设置为组表达式。  
  
 创建书签后，可以添加用户通过单击即可转到书签的报表项。 这些项通常为文本框或图像。  
  
 例如，如果报表显示按颜色分组的表，则可以向组头中添加基于组表达式的书签。 然后，即可在报表的开头处添加带有显示颜色值的单个文本框的表，并在该文本框上设置书签链接。 单击某种颜色时，报表就会跳至显示具有该颜色的组头行的页。  
  
 可以向任何报表项添加书签，也可以向具有 **“操作”** 属性的任何项添加书签链接，例如文本框、图像或图表中的计算序列。 有关详细信息，请参阅[“操作属性”对话框（报表生成器和 SSRS）](../action-properties-dialog-box-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-bookmark"></a>添加书签  
  
1.  在报表设计视图中，选择要向其添加书签的文本框、图像、图表或其他报表项。 所选项的属性将显示在“属性”窗格中。  
  
2.  在 **“书签”** 旁的文本框中，键入作为此书签的标签的字符串。 例如，可以键入 **BikePhoto** 作为报表中图像的书签。 此外，也可以单击表达式 (fx) 按钮打开“表达式”对话框，指定一个计算结果为标签的表达式。 对于组，键入的表达式应为组表达式。  
  
    > [!NOTE]  
    >  书签可以为任意字符串，但在报表中必须是唯一的。 如果书签不是唯一的，则指向该书签的链接将跳至第一个匹配书签。  
  
### <a name="to-add-a-bookmark-link"></a>添加书签链接  
  
1.  在“设计”视图中，右键单击要向其添加链接的文本框、图像或图表，然后单击“属性”。  
  
2.  在该报表项的 **“属性”** 对话框中，单击 **“操作”**。  
  
3.  选择 **“转到书签”**。 其他部分将显示在此选项的对话框中。  
  
4.  在 **“选择书签”** 框中，键入或选择一个书签或一个计算结果为书签的表达式。 在上一个示例中，可以键入 **BikePhoto** 为报表中的图像创建链接。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  （可选）文本的格式不会自动设置为链接。 对于文本，很有必要更改文本的颜色和效果以指示该文本是一个链接。 例如，在功能区的“主页”选项卡中的 **“字体”** 部分中，将颜色更改为蓝色，并将效果更改为下划线。  
  
7.  若要测试该链接，请单击 **“运行”** 以预览报表，然后单击对其设置此链接的报表项。  
  
## <a name="see-also"></a>请参阅  
 [交互式排序、文档结构图和链接（报表生成器和 SSRS）](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [筛选、 分组和对数据进行排序&#40;报表生成器和 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
