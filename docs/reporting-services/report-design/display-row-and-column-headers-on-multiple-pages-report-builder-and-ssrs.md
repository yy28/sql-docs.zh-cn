---
title: 在多个页中显示行标题和列标题（报表生成器）| Microsoft Docs
description: 可以控制跨多个页的 Tablix 数据区域（表、矩阵或列表）的 Reporting Services 分页报表的每页上是否重复行标题和列标题。
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.date: 12/09/2019
ms.openlocfilehash: ca1b00d98c71808cd42acb220e7fbf5d1c382555
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254595"
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>在多个页中显示行标题和列标题（报表生成器和 SSRS）

  可以控制跨多个页的 Tablix 数据区域（表、矩阵或列表）的 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页式报表的每页上是否重复行标题和列标题。
  
 控制行和列的方式取决于 Tablix 数据区域是否具有组头。 在包含组头的 Tablix 数据区域中单击时，点线将显示 Tablix 区域，如下图所示：  
  
 ![Tablix 数据区域](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix 数据区域")  
  
 通过使用新建表或矩阵向导或者新建图表向导，向“分组”窗格添加字段或使用上下文菜单添加组时，将自动创建行组标头和列组标头。 如果 Tablix 数据区域只包含 Tablix 正文区域，而没有组头，则行和列为 Tablix 成员。  
  
 对于静态成员，您可以在多个页面上显示顶部相邻的行或侧面相邻的列。  
  
## <a name="to-display-row-headers-on-multiple-pages"></a>在多个页上显示行标题  
  
1. 右键单击 Tablix 数据区域的行控点、列控点或角部控点，然后单击 **“Tablix 属性”** 。  
  
2. 在 **“行标题”** 中，选择 **“在每一页上重复标题行”** 。  
  
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-display-column-headers-on-multiple-pages"></a>在多个页上显示列标题  
  
1. 右键单击 Tablix 数据区域的行控点、列控点或角部控点，然后单击 **“Tablix 属性”** 。  
  
2. 在 **“列标题”** 中，选择 **“在每一页上重复标题列”** 。  
  
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-display-a-static-row-or-column-on-multiple-pages"></a>在多个页面上显示静态行或列  
  
1. 在设计图面上，单击 Tablix 数据区域中的行控点或列控点以将其选定。 “分组”窗格随即显示行组和列组。  
  
2. 在“分组”窗格的右侧，单击下箭头，然后单击 **“高级模式”** 。 “行组”窗格显示行组层次结构的层次结构静态和动态成员，而“列组”窗格显示列组层次结构的相同内容。  
  
3. 单击与在滚动时要使其保持可见的静态成员（行或列）相对应的静态成员。 “属性”窗格显示 **“Tablix 成员”** 属性。  
  
     如果未显示“属性”窗格，请单击报表生成器窗口顶部的“视图”选项卡，然后单击“属性”   。  
  
4. 在“属性”窗格中，将 **RepeatOnNewPage** 设置为 True。  
  
5. 将 **“KeepWithGroup”** 设为 After。  
  
6. 为要重复此出现的任意多个相邻成员重复此步骤。  
  
7. 预览报表。  
  
 当您查看 Tablix 数据区域分布的报表的每一页时，静态 Tablix 成员将在每页中重复出现。  
  
## <a name="see-also"></a>另请参阅  
 [查找、查看和管理报表（报表生成器和 SSRS）](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [控制分页符、标题、列和行（报表生成器和 SSRS）](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [与组一起显示组头和组尾（报表生成器和 SSRS）](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [在滚动报表时保持标题可见（报表生成器和 SSRS）](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  
