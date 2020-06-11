---
title: 了解数据库架构 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Schema Generation Wizard, database schema
- database schema [Analysis Services]
- relational schema [Analysis Services], database schema
- subject area schema options [Analysis Services]
- staging area schema options [Analysis Services]
- denormalized schemas
ms.assetid: 51e411f9-ee3f-4b92-9833-c2bce8c6b752
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9cf2e37d9a6ae6d0fa93012f72673642d11a2a4c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547449"
---
# <a name="understanding-the-database-schemas"></a>了解数据库架构
  架构生成向导为基于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的维度和度量值组的主题区域数据库生成一个非规范化的关系架构。 该向导为每个维度生成一个用于存储维度数据的关系表（该表称为维度表）；为每个度量值组生成一个用于存储事实数据的关系表（该表称为事实数据表）。 该向导在生成这些关系表时，会忽略链接维度、链接度量值组以及服务器时间维度。  
  
## <a name="validation"></a>验证  
 在架构生成向导开始生成基础关系架构之前，它会验证 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据集和维度。 如果该向导检测到错误，它便会停止并将错误报告到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的“任务列表”窗口。 阻止生成的错误示例包括：  
  
-   具有多个键属性的维度。  
  
-   具有键属性以外其他数据类型的父属性。  
  
-   没有度量值的度量值组。  
  
-   未正确配置的退化维度或度量值。  
  
-   未正确配置的代理键，如使用 `ScdOriginalID` 属性类型的多个属性，或使用未用整数数据类型绑定到列的 `ScdOriginalID` 的属性。  
  
## <a name="dimension-tables"></a>维度表  
 对于每个维度，架构生成向导都会生成一个要包含在主题区域数据库中的维度表。 维度表的结构取决于在设计它所基于的维度时所做的选择。  
  
 列  
 向导将为与维度表所基于的维度中的每个特性关联的绑定（例如，每个特性的 `KeyColumns`、`NameColumn`、`ValueColumn`、`CustomRollupColumn`、`CustomRollupPropertiesColumn` 和 `UnaryOperatorColumn` 等属性的绑定）生成一列。  
  
 关系  
 向导将生成每个父属性的列与维度表的主键之间的关系。  
  
 如果适用，向导还会生成在多维数据集中被定义为被引用维度的每个附加维度表中主键的关系。  
  
 约束  
 默认情况下，向导会为基于维度键属性的每个维度表生成一个主键约束。 如果生成了主键约束，则会在默认情况下生成一个单独的名称列。 逻辑主键在数据源视图中创建，即使您决定不在数据库中创建主键也是如此。  
  
> [!NOTE]  
>  如果在维度表所基于的维度中指定了多个键属性，则会出现错误。  
  
 翻译  
 向导会生成一个单独的表以保存需要翻译列的任意属性的翻译值。 向导还会为每种所需的语言创建一个单独的列。  
  
## <a name="fact-tables"></a>事实数据表  
 对于多维数据集中的每个度量值组，架构生成向导都会生成一个要包含在主题区域数据库中的事实数据表。 事实数据表的结构取决于在设计它所基于的度量值组时所做的选择，以及在度量值组和任何包含的维度之间建立的关系。  
  
 列  
 除了使用 `Count` 聚合函数的度量值以外，向导为每个度量值生成一列。 此类度量值在事实数据表中不需要对应的列。  
  
 如果适用，向导还会为度量值组中每个常规维度关系的每个粒度属性列生成一列；为与维度（与该表基于的度量值组具有事实维度关系）的每个属性关联的绑定生成一列或多列。  
  
 关系  
 向导会为每个从事实数据表到维度表的粒度属性的常规维度关系生成一种关系。 如果粒度基于维度表的键属性，则在数据库和数据源视图中创建关系。 如果粒度基于其他属性，则仅在数据源视图中创建关系。  
  
 如果选择在向导中生成索引，则会为这些关系列中的每个关系列生成非聚集索引。  
  
 约束  
 主键不会在事实数据表中生成。  
  
 如果您选择强制实施引用完整性，则会在适当的时候，在维度表和事实数据表之间生成引用完整性约束。  
  
 翻译  
 向导会生成一个单独的表以保存度量值组中需要翻译列的任意属性的翻译值。 向导还会为每种所需的语言创建一个单独的列。  
  
## <a name="data-type-conversion-and-default-lengths"></a>数据类型转换和默认长度  
 架构生成向导会在所有情况下忽略数据类型，但使用数据类型的列除外 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `wchar` 。 `wchar` 数据大小直接翻译为 `nvarchar` 数据类型。 但是，如果使用 `wchar` 大小的列的指定长度大于 4000 字节，则架构生成向导会生成一个错误。  
  
 如果数据项（如属性的绑定）没有指定的长度，则针对该列使用下表中列出的默认长度。  
  
|数据项|默认长度（字节）|  
|---------------|------------------------------|  
|KeyColumn|50|  
|NameColumn|50|  
|CustomRollupColumn|3000|  
|CustomRollupPropertiesColumn|500|  
|UnaryOperatorColumn|1|  
  
## <a name="see-also"></a>另请参阅  
 [了解增量生成](understanding-incremental-generation.md)   
 [管理对数据源视图和数据源所做的更改](manage-changes-to-data-source-views-and-data-sources.md)  
  
  
