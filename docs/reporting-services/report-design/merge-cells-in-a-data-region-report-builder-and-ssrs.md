---
title: "合并数据区域 （报表生成器和 SSRS） 中的单元 |Microsoft 文档"
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
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c643b94c86109a99e1448093b4b9744924fcd7f7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>合并数据区域中的单元（报表生成器和 SSRS）
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中，可通过合并数据区域中的单元来合并多个单元、改善数据区域外观或者为列组和行组提供跨越式标签。  
  
只能合并数据区域中同一个区内的单元，这些区包括：角部、列标题、组定义（或行标题）和正文。 不能合并跨区边界的单元。 例如，不能将数据区域角部区中的单元与行组区中的单元合并在一起。 有关详细信息，请参阅 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-merge-cells-in-a-data-region"></a>合并数据区域中的单元  
  
1.  在报表设计图面的数据区域中，单击第一个要合并的单元。 按住鼠标左键，垂直或水平拖动以选择相邻单元。 所选单元会突出显示。  
  
2.  右键单击选定的单元格，然后选择**合并单元格**。 所选单元将合并为一个单元。  
  
3.  重复步骤 1 和 2 可合并数据区域中的其他相邻单元。  
  
## <a name="see-also"></a>另请参阅  
[Tablix 数据区域](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)  
 [表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [创建矩阵](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [创建带列表的发票和表单](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
[表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  

