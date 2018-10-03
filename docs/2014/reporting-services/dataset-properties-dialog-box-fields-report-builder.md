---
title: 数据集属性对话框中，字段 （报表生成器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10021"
ms.assetid: 75c7e54a-3d20-4c9a-88da-ab36dce2ce42
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1dcbab871d5353d4f42183e89fadb6e83ed52e1d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116923"
---
# <a name="dataset-properties-dialog-box-fields-report-builder"></a>“数据集属性”对话框 -&gt;“字段”（报表生成器）
  在 **“数据集属性”** 对话框中选择 **“字段”** 可更改报表数据集的字段集合。 尽管字段列表是自动填充的，但是可以使用 **“字段”** 来添加、编辑和删除查询及计算字段。  
  
 仅在嵌入数据集上支持计算字段。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>选项  
 **“添加”**  
 向数据集添加新的查询或计算字段。  
  
 **删除**  
 从数据集中删除所选字段。  
  
 **字段名称**  
 为字段键入名称。 该字段在数据集中必须是唯一的。 对于数据集中的每个现有字段，名称是预先填充的。  
  
 **字段源**  
 为字段输入一个值。  
  
 对于计算字段，字段源必须是由数据集查询检索的现有字段的名称或您所创建的表达式。 例如，若要创建表示 10 倍于查询字段 Sales 中值的字段，请使用表达式 `=10 * Fields!Sales.Value`。  
  
 对于查询字段，字段源必须是由数据集查询检索的现有字段的名称。  
  
 **表达式 (fx)**  
 为新的计算字段添加或更改表达式。 仅当单击 **“添加”** 并选择 **“计算字段”** 时，才会显示此按钮。  
  
## <a name="see-also"></a>请参阅  
 [数据集字段集合（报表生成器和 SSRS）](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [用于对话框、窗格和向导的报表生成器帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [数据集属性对话框中，选项&#40;报表生成器&#41;](report-data/dataset-properties-dialog-box-options-report-builder.md)   
 [数据集属性对话框中，筛选器&#40;报表生成器&#41;](../../2014/reporting-services/dataset-properties-dialog-box-filters-report-builder.md)   
 [数据集属性对话框中，参数&#40;报表生成器&#41;](../../2014/reporting-services/dataset-properties-dialog-box-parameters-report-builder.md)   
 [数据集属性对话框中，查询&#40;报表生成器&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [表达式（报表生成器和 SSRS）](report-design/expressions-report-builder-and-ssrs.md)   
 [报表生成器中的数据连接、数据源和连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
