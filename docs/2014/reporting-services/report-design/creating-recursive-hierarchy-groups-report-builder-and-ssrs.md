---
title: 创建递归层次结构组 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 92412bbde8a1032b34264ca254560f31704281e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63135572"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>创建递归层次结构组 （报表生成器和 SSRS）
  若要显示递归数据，其中由数据集中的字段表示父级和子级之间的关系，可以设置数据区域组表达式根据子字段并设置基于父字段的父属性。  
  
 递归层次结构组，例如，员工在组织结构图中的一个常见用途是显示分层数据。 数据集包含雇员和经理，其中经理的姓名也显示在员工的列表中的列表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>创建递归层次结构  
 若要生成 tablix 数据区域中的递归层次结构，您必须设置为指定子数据和为指定父数据的字段组的父属性的字段，组表达式。 例如，对于包含雇员向经理，报告将组表达式设置为雇员 ID 和管理器的父属性的员工 ID 和经理 ID 字段的数据集，id。  
  
 定义为递归层次结构 （即，使用父属性的组） 的组可以具有一个组表达式。 可以在填充文本框时使用 `Level` 函数，根据员工在层次结构中的级别来缩进员工姓名。  
  
 有关详细信息，请参阅[添加或删除数据区域中的组&#40;报表生成器和 SSRS&#41; ](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)并[创建递归层次结构组&#40;报表生成器和 SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)。  
  
### <a name="aggregate-functions-that-support-recursion"></a>支持递归的聚合函数  
 可以使用接受参数的 Reporting Services 聚合函数*递归*来计算递归层次结构的摘要数据。 以下函数接受`Recursive`作为参数：[总和](report-builder-functions-sum-function.md)， [Avg](report-builder-functions-avg-function.md)，[计数](report-builder-functions-count-function.md)， [CountDistinct](report-builder-functions-countdistinct-function.md)， [CountRows](report-builder-functions-countrows-function.md)， [Max](report-builder-functions-max-function.md)， [Min](report-builder-functions-min-function.md)， [StDev](report-builder-functions-stdev-function.md)， [StDevP](report-builder-functions-stdevp-function.md)， [Sum](report-builder-functions-sum-function.md)， [Var](report-builder-functions-var-function.md)，和[VarP](report-builder-functions-varp-function.md). 有关详细信息，请参阅[聚合函数引用&#40;报表生成器和 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)。  
  
## <a name="see-also"></a>请参阅  
 [表、 矩阵和列表&#40;报表生成器和 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tablix 数据区域&#40;报表生成器和 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [聚合函数参考&#40;报表生成器和 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [表&#40;报表生成器和 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [矩阵&#40;报表生成器和 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [列出了&#40;报表生成器和 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [表、 矩阵和列表&#40;报表生成器和 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
