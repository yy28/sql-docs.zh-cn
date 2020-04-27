---
title: 在多个页中显示行标题和列标题（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2422b1e2-822f-4379-9d7f-9afebb350e3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8b5b343a32480d7d8ae59e9fa27fbe7d1f531213
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106014"
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>在多个页中显示行标题和列标题（报表生成器和 SSRS）
  您可以控制在跨越多个页的 Tablix 数据区域的每个页上是否重复行标题和列标题。 Tablix 数据区域可以是一个表、矩阵或列表。  
  
 控制行和列的方式取决于 Tablix 数据区域是否具有组头。 在包含组头的 Tablix 数据区域中单击时，点线将显示 Tablix 区域，如下图所示：  
  
 ![Tablix 数据区域](../media/rs-tablixareas.gif "Tablix 数据区域")  
  
 通过使用新建表或矩阵向导或者新建图表向导，向“分组”窗格添加字段或使用上下文菜单添加组时，将自动创建行组标头和列组标头。 如果 Tablix 数据区域只包含 Tablix 正文区域，而没有组头，则行和列为 Tablix 成员。  
  
 对于静态成员，您可以在多个页面上显示顶部相邻的行或侧面相邻的列。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-row-headers-on-multiple-pages"></a>在多个页上显示行标题  
  
1.  右键单击 Tablix 数据区域的行控点、列控点或角部控点，然后单击 **“Tablix 属性”** 。  
  
2.  在 **“行标题”** 中，选择 **“在每一页上重复标题行”** 。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-column-headers-on-multiple-pages"></a>在多个页上显示列标题  
  
1.  右键单击 Tablix 数据区域的行控点、列控点或角部控点，然后单击 **“Tablix 属性”** 。  
  
2.  在 **“列标题”** 中，选择 **“在每一页上重复标题列”** 。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-a-static-tablix-member-row-or-column-on-multiple-pages"></a>在多个页面上显示静态 Tablix 成员（行或列）  
  
1.  在设计图面上，单击 Tablix 数据区域中的行控点或列控点以将其选定。 “分组”窗格随即显示行组和列组。  
  
2.  在“分组”窗格的右侧，单击下箭头，然后单击 **“高级模式”** 。 “行组”窗格显示行组层次结构的层次结构静态和动态成员，而“列组”窗格显示列组层次结构的相同内容。  
  
3.  单击与在滚动时要使其保持可见的静态成员（行或列）相对应的静态成员。 “属性”窗格显示 **“Tablix 成员”** 属性。  
  
     如果未显示“属性”窗格，请单击报表生成器窗口顶部的“视图”选项卡，然后单击“属性”   。  
  
4.  在“属性”窗格中，将 **RepeatOnNewPage** 设置为 True。  
  
5.  将 **“KeepWithGroup”** 设为 After。  
  
6.  为要重复此出现的任意多个相邻成员重复此步骤。  
  
7.  预览报表。  
  
 当您查看 Tablix 数据区域分布的报表的每一页时，静态 Tablix 成员将在每页中重复出现。  
  
## <a name="see-also"></a>另请参阅  
 [查找、查看和管理报表（报表生成器和 SSRS）](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [导出报表 &#40;报表生成器和 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [控制分页符、标题、列和行（报表生成器和 SSRS）](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [与组一起显示组头和组尾（报表生成器和 SSRS）](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [在滚动报表时保持标题可见（报表生成器和 SSRS）](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  
