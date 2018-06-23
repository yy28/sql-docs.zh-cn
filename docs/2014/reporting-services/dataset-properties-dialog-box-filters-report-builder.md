---
title: 数据集属性对话框中，筛选器 （报表生成器） |Microsoft 文档
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
- "10025"
ms.assetid: 933a6f44-4eb7-4e73-9c40-ac0fd17b23d3
caps.latest.revision: 14
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: beb0703212eb639483bbaa015b6fa89bba3a3068
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013829"
---
# <a name="dataset-properties-dialog-box-filters-report-builder"></a>“数据集属性”对话框 ->“筛选器”（报表生成器）
  在 **“数据集属性”** 对话框中选择 **“筛选器”** 可创建数据集的筛选器。  
  
 作为报表服务器上共享数据集定义一部分的筛选器会影响使用此共享数据集的所有报表。 在将共享数据集添加到报表后，可以为其指定其他筛选器。 这些筛选器只会影响在其中定义它们的报表。  
  
 嵌入数据集的筛选器只会影响在其中定义它们的报表。  
  
 有关详细信息，请参阅[对数据进行筛选、分组和排序（报表生成器和 SSRS）](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>“常规”  
 **“添加”**  
 向列表中添加新的筛选子句。  
  
 **删除**  
 从列表中删除选定的筛选子句。  
  
 **向上键**  
 在列表中向上移动所选的筛选器。  
  
 **向下键**  
 在列表中向下移动所选的筛选器。  
  
 **表达式**  
 键入或选择要对其应用筛选器的表达式。 单击“表达式”(**fx**) 按钮可编辑表达式。  
  
 **Data type**  
 为“值”选择数据类型。 如果可能，请选择与 **“表达式”** 的数据类型匹配的数据类型。  
  
 **“表达式”** 和 **“值”** 中的值的计算结果必须属于同一数据类型。 例如，如果“表达式”设置为具有数据类型 System.Int32 的字段并且“值”设置为 7，则从下拉列表中选择 **Integer**。  
  
 如果您需要的数据类型选项不在下拉列表中，请编写表达式将该值转换成正确的数据类型。 有关详细信息，请参阅[筛选器公式示例（报表生成器和 SSRS）](report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
 **“运算符”**  
 选择要用于比较表达式和值的运算符。  
  
 **ReplTest1**  
 键入在计算“表达式”框中所指定的表达式时要使用的表达式或值。 单击“表达式”(**fx**) 按钮可编辑表达式。  
  
## <a name="see-also"></a>请参阅  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [报表参数（报表生成器和报表设计器）](report-design/report-parameters-report-builder-and-report-designer.md)   
 [向数据集添加筛选器&#40;报表生成器和 SSRS&#41;](report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)   
 [在报表中使用表达式&#40;报表生成器和 SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  