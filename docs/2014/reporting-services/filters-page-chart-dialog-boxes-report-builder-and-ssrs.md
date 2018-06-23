---
title: 筛选器页，图表对话框 （报表生成器和 SSRS） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.categorygroupproperties.filters.f1
- "10409"
- sql12.rtp.rptdesigner.seriesgroupproperties.filters.f1
- "10401"
- sql12.rtp.rptdesigner.chartproperties.filters.f1
- "10165"
ms.assetid: fab97b2f-d53f-42f2-900c-c159653d89ed
caps.latest.revision: 14
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 5b695b45a43f388a7dabf64bad327404ef4f6510
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124271"
---
# <a name="filters-page-chart-dialog-boxes-report-builder-and-ssrs"></a>“筛选器”页 -&gt;“图表”对话框（报表生成器和 SSRS）
  在以下对话框中单击 **“筛选器”** ：  
  
-   **“类别组属性”** 对话框：可以对已按类别分组的序列中的数据点进行筛选。  
  
-   **“图表属性”** 对话框：可以定义图表的筛选选项。  
  
-   **“序列组属性”** 对话框：可以限制所选组中的序列数。  
  
## <a name="options"></a>“常规”  
 **“添加”**  
 单击此选项可向列表中添加新的筛选子句。  
  
 **删除**  
 单击此选项可从列表中删除选定的筛选子句。  
  
 **向上键**  
 单击此选项可在列表中向上移动所选的筛选器。  
  
 **向下键**  
 单击此选项可在列表中向下移动所选的筛选器。  
  
 **表达式**  
 键入或选择要对其应用筛选器的表达式。 单击“表达式”(**fx**) 按钮可编辑表达式。  
  
 **Data type**  
 为“值”选择数据类型。 如果可能，请选择与 **“表达式”** 的数据类型匹配的数据类型。  
  
 **“表达式”** 和 **“值”** 中的值的计算结果必须属于同一数据类型。 例如，如果“表达式”设置为具有数据类型 System.Int32 的字段并且“值”设置为 7，则从下拉列表中选择 **Integer**。  
  
 如果您需要的数据类型选项不在下拉列表中，请编写表达式将该值转换成正确的数据类型。 有关详细信息，请参阅[筛选器公式示例（报表生成器和 SSRS）](report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
 **“运算符”**  
 选择要用于比较表达式和值的运算符。  
  
 **ReplTest1**  
 键入对“表达式”中的表达式进行计算时所依据的表达式或值。  
  
## <a name="see-also"></a>请参阅  
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [表达式示例（报表生成器和 SSRS）](report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](report-design/expressions-report-builder-and-ssrs.md)   
 [筛选、 分组和排序数据&#40;报表生成器和 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  