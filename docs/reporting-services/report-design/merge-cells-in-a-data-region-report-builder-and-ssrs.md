---
title: 合并数据区域中的单元（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e01f1aa9fb11f84f1b5efe2e0f5a63fe7fde5fb4
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297245"
---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>合并数据区域中的单元（报表生成器和 SSRS）
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中，可通过合并数据区域中的单元来合并多个单元、改善数据区域外观或者为列组和行组提供跨越式标签。  
  
只能合并数据区域中同一个区内的单元，这些区包括：角部、列标题、组定义（或行标题）和正文。 不能合并跨区边界的单元。 例如，不能将数据区域角部区中的单元与行组区中的单元合并在一起。 有关详细信息，请参阅 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-merge-cells-in-a-data-region"></a>合并数据区域中的单元  
  
1.  在报表设计图面的数据区域中，单击第一个要合并的单元。 按住鼠标左键，垂直或水平拖动以选择相邻单元。 所选单元会突出显示。  
  
2.  右键单击所选单元并选择“合并单元”。 所选单元将合并为一个单元。  
  
3.  重复步骤 1 和 2 可合并数据区域中的其他相邻单元。  
  
## <a name="see-also"></a>另请参阅  
[Tablix 数据区域](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)  
 [表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [创建矩阵](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [创建带列表的发票和表单](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
[表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
