---
title: 切片源多维数据集 （数据挖掘向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.slicesourcecube.f1
ms.assetid: 16485608-d3b9-49ee-8baa-948038cdd7ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c68ec29c2461cb7ffddfdbd2792e1a1a191076b2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416648"
---
# <a name="slice-source-cube-data-mining-wizard"></a>对源多维数据集进行切片（数据挖掘向导）
   可以使用“对源多维数据集进行切片”对话框限制用于为模型定型的数据。 通常一个多维数据集包含与很多不同维度和属性有关的数据，例如所有商店、所有区域和所有产品。 定型无限的属性组合的模型是不现实的，因此您使用此对话框选择要在定型模型中使用的特定集合。  
  
 例如，在 AdventureWorks 多维数据集中，您可能按特定产品线、区域或年份切片以获取某部分数据。  
  
 如果不熟悉切片和多维数据集，我们建议你查看以下这些文章：  
  
-   [设置分区切片属性&#40;Analysis Services&#41;](multidimensional-models/set-the-partition-slice-property-analysis-services.md)  
  
-   [创建和管理本地分区 (Analysis Services)](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
> [!NOTE]  
>  请注意，动态 MDX 函数（如 [Generate (MDX)](/sql/mdx/generate-mdx) 或 [Except (MDX)](/sql/mdx/except-mdx-function)）在分区的切片属性中不受支持。 你必须通过使用显式元组或成员引用定义切片。  
>   
>  例如，而不是使用[:&#40;范围&#41; &#40;MDX&#41; ](/sql/mdx/range-mdx)可以定义的范围，你需要枚举分属特定年份的每个成员。  
>   
>  如果需要定义复杂的切片，我们建议使用 XMLA Alter 脚本在切片中定义元组。 然后，你可以使用 ascmd 命令行工具或 SSIS [Analysis Services Execute DDL Task](../integration-services/control-flow/analysis-services-execute-ddl-task.md) 运行该脚本并立即创建指定的成员集，之后再处理分区。  
  
 **有关详细信息：**[数据挖掘向导&#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md)，[创建关系挖掘结构](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>选项  
 **Dimension**  
 选择要进行切片的维度。  
  
 **Hierarchy**  
 选择要进行切片的层次结构。 您可以选择任意的层级结构级别，但是在模型中使用的属性将仅位于您选择的级别。  
  
 例如，如果您选择“地理”层次结构，选择“国家/地区”作为级别，则不能生成使用“城市”作为属性的模型。 相反，如果您选择“城市”作为对其切片的层次结构级别，则不能创建基于“国家/地区”的挖掘模型。  
  
 **“运算符”**  
 选择要在生成切片表达式中使用的运算符。  
  
 例如，如果你选择在层次结构的地理位置，您可以选择运算符 =，然后键入"Europe"作为筛选器，以仅获取欧洲的多维数据集数据。  
  
 **筛选表达式**  
 键入要作为针对所选维度筛选多维数据集时的标准的表达式。  
  
 **Parameters**  
 此选项不用于数据挖掘模型。  
  
## <a name="see-also"></a>请参阅  
 [完成向导&#40;数据挖掘向导&#41;](completing-the-wizard-data-mining-wizard.md)   
 [数据挖掘向导的 F1 帮助&#40;Analysis Services-数据挖掘&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [指定挖掘模型列用法&#40;数据挖掘向导&#41;](specify-mining-model-column-usage-data-mining-wizard.md)  
  
  
