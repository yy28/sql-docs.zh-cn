---
title: 数据集属性对话框，参数 （报表生成器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10023"
ms.assetid: 3a0672ad-c969-455b-b952-585164ce1dda
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 295a40bc7964e50e5fc0c4a9ea0294b593fdde18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109384"
---
# <a name="dataset-properties-dialog-box-parameters-report-builder"></a>“数据集属性”对话框 -&gt;“参数”（报表生成器）
  选择**参数**上**数据集属性**对话框可以添加、 更改和删除查询参数。  
  
 对于嵌入数据集，选项应用于报表定义中的数据集。  
  
 对于共享数据集，选项应用于报表服务器上的共享数据集定义。  
  
 有关详细信息，请参阅[嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>选项  
 **“添加”**  
 将新的参数添加到列表。  
  
 **删除**  
 从列表中删除所选参数。  
  
 **向上键**  
 在列表中向上移动所选的参数。  
  
 **向下键**  
 在列表中向下移动所选的参数。  
  
 **参数名称**  
 键入添加到“数据集属性”  对话框“查询”  选项卡上数据集中的查询参数的名称。  
  
 **参数值**  
 仅限嵌入数据集。  
  
 输入查询参数的值。 此值既可以是静态值，也可以是引用报表内对象的表达式（但不能引用任何报表项或字段）。 默认情况下， **“值”** 中包含指向报表参数的表达式。  
  
 **默认值**  
 仅限共享数据集。  
  
 选中此复选框可以指定默认值。  
  
 输入默认值。 该值可以是静态值或引用报表中的对象的表达式。 该表达式不能引用报表项、报表参数或字段。  
  
 若要指定空白，请将文本框保留为空。  
  
 若要指定 Null，请选择“可以为 Null”选项。  
  
 **只读**  
 仅限共享数据集。  
  
 选择此选项可在共享数据集定义中将此参数标记为只读。 在将共享数据集添加到报表时，该参数不出现在属性中。 在报表服务器上缓存共享数据集时，不能更改该值。  
  
 **可以为 Null**  
 仅限共享数据集。  
  
 选择此选项可允许 Null 值。  
  
 **从查询中省略**  
 仅限共享数据集。  
  
 当对报表参数的引用位于共享数据集筛选器的表达式中而非查询中时，选择此选项。 在您选择此选项后，无需在查询运行时为此参数指定默认值。  
  
## <a name="see-also"></a>请参阅  
 [用于对话框、窗格和向导的报表生成器帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [数据集属性对话框中，查询&#40;报表生成器&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [表达式（报表生成器和 SSRS）](report-design/expressions-report-builder-and-ssrs.md)   
 [教程：向报表添加参数（报表生成器）](tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [报表参数（报表生成器和报表设计器）](report-design/report-parameters-report-builder-and-report-designer.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [查询设计器（报表生成器）](../../2014/reporting-services/query-designers-report-builder.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
  
