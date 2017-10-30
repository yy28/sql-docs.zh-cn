---
title: "创建递归层次结构组 （报表生成器和 SSRS） |Microsoft 文档"
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
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b6f587b40c53ff64b484b86a324b92ca5de21b77
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>创建递归层次结构组（报表生成器和 SSRS）
若要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中显示递归数据（其中父级和子级之间的关系由数据集中的字段表示），则可以根据子字段设置数据区域组表达式，根据父字段设置 Parent 属性。  
  
 递归层次结构组通常用于显示分层数据，例如，显示组织结构图中的雇员。 数据集包含雇员和经理的列表，其中经理的姓名也显示在雇员列表中。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>创建递归层次结构  
 若要在 Tablix 数据区域中创建一个递归层次结构，必须将组表达式设置为指定子数据的字段，并将该组的 Parent 属性设置为指定父数据的字段。 例如，对于包含雇员 ID 字段和经理 ID 字段的数据集（其中雇员向经理报告），将组表达式设置为雇员 ID，并将 Parent 属性设置为经理 ID。  
  
 定义为递归层次结构的组（即使用 Parent 属性的组）只能有一个组表达式。 您可以在文本框填充中使用 **Level** 函数，以便基于雇员在层次结构中的级别来缩进雇员姓名。  
  
 有关详细信息，请参阅[添加或删除数据区域 &#40; 中的组报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)和[创建递归层次结构组 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>支持递归的聚合函数  
 可以使用接受 *Recursive* 参数的 Reporting Services 聚合函数来计算递归层次结构的汇总数据。 下列函数接受 **Recursive** 参数： [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md)、 [Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md)、 [Count](../../reporting-services/report-design/report-builder-functions-count-function.md)、 [CountDistinct](../../reporting-services/report-design/report-builder-functions-countdistinct-function.md)、 [CountRows](../../reporting-services/report-design/report-builder-functions-countrows-function.md)、 [Max](../../reporting-services/report-design/report-builder-functions-max-function.md)、 [Min](../../reporting-services/report-design/report-builder-functions-min-function.md)、 [StDev](../../reporting-services/report-design/report-builder-functions-stdev-function.md)、 [StDevP](../../reporting-services/report-design/report-builder-functions-stdevp-function.md)、 [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md)、 [Var](../../reporting-services/report-design/report-builder-functions-var-function.md)和 [VarP](../../reporting-services/report-design/report-builder-functions-varp-function.md)。 有关详细信息，请参阅 [聚合函数引用（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tablix 数据区域 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [聚合函数引用 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩阵 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [列表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)    
 [表、 矩阵和列表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  

