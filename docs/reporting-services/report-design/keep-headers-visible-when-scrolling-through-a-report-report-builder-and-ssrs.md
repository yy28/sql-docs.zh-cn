---
title: 在滚动报表时保持标题可见（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 710b0d5be1521aed0a5ba79166e1d050b1f90c62
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33023404"
---
# <a name="keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs"></a>在滚动报表时保持标题可见（报表生成器和 SSRS）
  呈现报表之后，为防止行和列标签滚动出视野之外，可以冻结行或列标题。  
  
 控制行和列的方式取决于您是拥有表还是矩阵。 如果您拥有表，则将静态成员（行标题和列标题）配置为保持可见。 如果您拥有矩阵，则将行组头和列组头配置为保持可见。  
  
 如果将报表导出到 Excel，则不会自动冻结标头。 可以冻结 Excel 中的窗格。 有关详细信息，请参阅[导出到 Microsoft Excel（报表生成器和 SSRS）](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)的“页眉和页脚”节。  
  
> [!NOTE]  
>  即使表拥有行组和列组，也不能使这些组头在滚动时保持可见  
  
 下图显示了一个表。  
  
 ![表](../../reporting-services/report-design/media/table.png "Table")  
  
 下图显示了一个矩阵。  
  
 ![矩阵](../../reporting-services/report-design/media/matrix.png "Matrix")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-matrix-group-headers-visible-while-scrolling"></a>使矩阵组头在滚动时保持可见  
  
1.  右键单击 Tablix 数据区域的行控点、列控点或角部控点，然后单击 **“Tablix 属性”**。  
  
2.  在 **“常规”** 选项卡上的 **“行标题”** 或 **“列标题”** 下选择 **“滚动时标题应保持可见”**。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-keep-a-static-tablix-member-row-or-column-visible-while-scrolling"></a>滚动时保持静态 Tablix 成员（行或列）可见  
  
1.  在设计图面上，单击表中任意位置，可在分组窗格中显示静态成员及组。  
  
     ![“分组”窗格](../../reporting-services/report-design/media/grouppane-updated.png "Grouping pane")  
  
     “行组”窗格显示行组层次结构的层次结构静态和动态成员，而“列组”窗格显示列组层次结构的相同内容。  
  
2.  在“分组”窗格的右侧，单击下箭头，然后单击 **“高级模式”**。  
  
3.  单击要在滚动时保持可见的静态成员（行或列）。 “属性”窗格显示 **“Tablix 成员”** 属性。  
  
     ![Tablix 成员属性](../../reporting-services/report-design/media/grouppane-tablixmember-updated.png "Tablix Member properties")  
  
4.  在“属性”窗格中，将 **FixedData** 设置为 **True**。  
  
5.  对所有要在滚动时保持可见的相邻成员重复此过程。  
  
6.  预览报表。  
  
 对报表翻页或横向移动时，静态 Tablix 成员仍将可见。  
  
## <a name="see-also"></a>另请参阅  
 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [与组一起显示组头和组尾（报表生成器和 SSRS）](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [在多个页中显示行标题和列标题（报表生成器和 SSRS）](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [“分组”窗格（报表生成器）](../../reporting-services/report-design/grouping-pane-report-builder.md)  
  
  
