---
title: 表和列 (SSAS 表格) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c428d717-05de-436c-b9dc-e8c1925a60ca
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6f7302274fc745fbc7a63bf6af59e4622c36b9a0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013897"
---
# <a name="tables-and-columns-ssas-tabular"></a>表和列（SSAS 表格）
  在您通过使用表导入向导将表和数据添加到某一模型后，可通过添加新的数据列、创建表之间的关系、定义对数据进行扩展的计算以及对表中的数据进行筛选和排序以便于查看，开始使用这些表。  
  
 本主题的内容：  
  
-   [优势](#bkmk_benefits)  
  
-   [使用表和列](#bkmk_working)  
  
-   [相关任务](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 优势  
 在表格模型中，表提供在其中定义列和其他元数据的框架。 表包括：  
  
 **表定义**  
 表定义包括列组。 列可以从数据源导入，也可以手动添加，例如使用计算列。  
  
 **表元数据**  
 关系、度量值、角色、透视和粘贴的数据全都是在表的上下文内定义对象的元数据。  
  
 **Data**  
 在您通过使用表导入向导或通过在计算列中创建新数据来首次导入表时，将数据填充到表列中。 当源中的数据发生更改时，或者在从内存中删除某一模型时，必须运行某一处理操作以便将数据重新填充到表中。  
  
##  <a name="bkmk_working"></a> 使用表和列  
 在模型设计器中，您不直接创建新的模型表。 在从其他数据源导入或复制数据时，会自动为您创建新选项卡。 模型设计器中的每个选项卡都包含一个数据表，其中可能包括以下内容：  
  
-   来自关系数据库或其他非关系源（如 Analysis Services 多维数据集）的单个表或视图。  
  
-   从数据馈送或文本文件导入的表格形式的数据集合。  
  
-   关系数据和表格 (HTML) 数据的组合复制并粘贴到表中。  
  
 当您导入数据时，每个表或视图、工作表或数据文件都将作为表添加到模型设计器中。 通常，来自不同数据源的数据添加到单独的选项卡上，但可以使用 **“粘贴”** 和 **“追加粘贴”** 将数据合并到一个表中。 有关详细信息，请参阅[复制并粘贴数据（SSAS 表格）](../copy-and-paste-data-ssas-tabular.md)。  
  
 在添加了所需的数据后，可以创建各表之间的其他关系，查找或引用其他表中的相关值，或者通过添加新的计算列创建派生值。  
  
 如果您在使用非常大的数据集，则可能要筛选出某些数据，以便这些数据不可见。 您还可能要按不同的顺序对数据进行排序。 通过使用模型设计器，您可以使用筛选、排序和隐藏功能来显示或不显示整个列或某些数据。  
  
##  <a name="bkmk_related_tasks"></a> 相关任务  
  
|主题|Description|  
|-----------|-----------------|  
|[向表中添加列&#40;SSAS 表格&#41;](add-columns-to-a-table-ssas-tabular.md)|介绍如何将源列添加到表定义。|  
|[删除列&#40;SSAS 表格&#41;](delete-a-column-ssas-tabular.md)|说明如何使用模型设计器或“表属性”对话框删除模型表列。|  
|[更改表、 列或行筛选器映射&#40;SSAS 表格&#41;](change-table-column-or-row-filter-mappings-ssas-tabular.md)|介绍如何通过使用表预览或 SQL 查询编辑器在“编辑表属性”对话框中更改表、列或行筛选器映射。|  
|[指定标记为日期表用于时间智能&#40;SSAS 表格&#41;](specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)|介绍如何使用“标记为日期表”对话框指定日期表和唯一标识符列。 在 DAX 公式中使用时间智能函数时，必须指定日期表和唯一标识符。|  
|[将表添加&#40;SSAS 表格&#41;](add-a-table-ssas-tabular.md)|介绍如何通过使用现有数据源连接从数据源中添加表。|  
|[删除表&#40;SSAS 表格&#41;](delete-a-table-ssas-tabular.md)|介绍如何删除不再需要的模型工作区数据库中的表。|  
|[重命名表或列&#40;SSAS 表格&#41;](rename-a-table-or-column-ssas-tabular.md)|介绍如何重命名表或列以使其在您的模型中更易于标识。|  
|[设置列的数据类型&#40;SSAS 表格&#41;](set-the-data-type-of-a-column-ssas-tabular.md)|介绍如何更改列的数据类型。 数据类型定义列中的数据是如何存储和展示的。|  
|[隐藏或冻结列&#40;SSAS 表格&#41;](hide-or-freeze-columns-ssas-tabular.md)|介绍如何隐藏您不想显示的列，以及如何通过冻结（锁定）一个区域中的特定列，在滚动到模型的其他区域时使模型的某一区域可见。|  
|[计算列&#40;SSAS 表格&#41;](ssas-calculated-columns.md)|本节中的主题介绍了如何使用计算列向您的模型添加聚合数据。|  
|[筛选和排序数据&#40;SSAS 表格&#41;](../filter-and-sort-data-ssas-tabular.md)|本节中的主题介绍了如何使用模型设计器中的控件对数据进行筛选或排序。|  
  
  