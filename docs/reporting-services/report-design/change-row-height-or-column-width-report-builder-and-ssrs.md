---
title: 更改行高或列宽（报表生成器和 SSRS）| Microsoft Docs
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
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c731a73e7d409bbc178901165140f694596887ce
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33020524"
---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>更改行高或列宽（报表生成器和 SSRS）
  设置行高时，您所指定的是呈现的报表中行的最大高度。 但默认情况下，行中的文本框设置为可在运行时沿垂直方向增长，以容纳其中的数据，这会使行超过您指定的高度。 若要设置固定行高，您必须更改文本框的属性，使其不会自动增高。  
  
 设置列宽时，您所指定的是呈现的报表中列的最大宽度。 列不会自动进行水平调整来容纳文本。  
  
 如果行或列中的单元格包含矩形或数据区域，则单元格的最小高度和宽度将由所含项的高度和宽度决定。 有关详细信息，请参阅[呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>通过移动行控点来更改行高  
  
1.  在“设计”视图中，单击 Tablix 数据区域中的任何位置以选中该区域。 Tablix 数据区域的外边框上将会出现灰色的行控点。  
  
2.  将鼠标悬停于要拉伸的行控点边缘上。 此时将会出现一个双向箭头。  
  
3.  单击以抓住行边缘，然后向上或向下移动行边缘，从而调整行高。  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>通过设置单元属性来更改行高  
  
1.  在设计视图中，单击表行中的单元。  
  
     ![表中的已选单元格](../../reporting-services/report-design/media/table-selectcell.png "Selected Cell in a Table")  
  
2.  在显示的“属性”  窗格中，修改“高度”  属性，然后单击“属性”  窗格外部的任意位置。  
  
     ![所选表单元格的“属性”窗格](../../reporting-services/report-design/media/cell-propertiespane.png "Properties Pane for selected table cell")  
  
### <a name="to-prevent-a-row-from-automatically-expanding-vertically"></a>防止行自动垂直增高  
  
1.  在“设计”视图中，单击 Tablix 数据区域中的任何位置以选中该区域。 Tablix 数据区域的外边框上将会出现灰色的行控点。  
  
2.  单击行控点以选中行。  
  
3.  在“属性”窗格中，将 CanGrow 设置为 **False**。  
  
    > [!NOTE]  
    >  如果没有看到“属性”窗格，请单击“视图”菜单上的“属性”。  
  
### <a name="to-change-column-width"></a>更改列宽  
  
1.  在“设计”视图中，单击 Tablix 数据区域中的任何位置以选中该区域。 Tablix 数据区域的外边框上将会出现灰色的列控点。  
  
2.  将鼠标悬停于要拉伸的列控点边缘上。 此时将会出现一个双向箭头。  
  
3.  单击以抓住列边缘，然后向左或向右移动列边缘，从而调整列宽。  
  
## <a name="see-also"></a>另请参阅  
 [Tablix 数据区域（报表生成器和 SSRS）](tablix-data-region-report-builder-and-ssrs.md)   
 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
