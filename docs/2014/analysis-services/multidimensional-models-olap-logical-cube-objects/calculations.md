---
title: 计算 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- calculations [Analysis Services]
- OLAP objects [Analysis Services], calculations
- MDX [Analysis Services], calculations
- calculations [Analysis Services], about calculations
- cubes [Analysis Services], calculations
ms.assetid: 6be84916-fd05-4efc-ab98-6adbbad80154
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4457a5fa434be3865edf770f7ca69a676c051893
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545339"
---
# <a name="calculations"></a>计算
  计算是一个多维表达式（MDX）表达式或脚本，用于在中的多维数据集中定义计算成员、命名集或作用域分配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 使用计算，您可以添加不是由多维数据集的数据而是由特定表达式（这些表达式可以引用多维数据集的其他部分、其他多维数据集，或者甚至引用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库以外的信息）所定义的对象。 使用计算，您还可以扩展多维数据集的功能，提高商业智能应用程序的灵活性和能力。 有关脚本计算的详细信息，请参阅[Microsoft SQL Server 2005 中的 MDX 脚本介绍](https://go.microsoft.com/fwlink/?LinkId=81892)。 有关与 MDX 查询和计算相关的性能问题的详细信息，请参阅[SQL Server 2005 Analysis Services 性能指南](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)。  
  
## <a name="calculated-members"></a>计算成员  
 计算成员是在运行时使用对其进行定义时所指定的多维表达式 (MDX) 表达式来计算其值的成员。 计算成员就像其他任何成员一样，可用于商业智能应用程序。 计算成员不会增加多维数据集的大小，因为多维数据集中只存储定义；值的计算则在需要回答查询时才在内存中执行。  
  
 可以为任何维度（包括度量值维度）定义计算成员。 在度量值维度中创建的计算成员称为计算度量值。  
  
 尽管计算成员通常基于多维数据集中已存在的数据，但是可以通过将数据与算术运算符、数字和函数进行组合而创建复杂的表达式。 还可以使用 MDX 函数（例如，LookupCube）来访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库内其他多维数据集中的数据。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括标准化 Visual Studio 函数库，可以使用存储过程从除当前 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库以外的源中检索数据。 有关存储过程的详细信息，请参阅[定义存储过程](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)。  
  
 例如，假设货运公司的行政人员希望基于每体积单位的利润确定运输哪种类型的货物利润更高。 他们使用包含“货物”、“船队”和“时间”维度以及 Price_to_Ship、Cost_to_Ship 和 Volume_in_Cubic_Meters 度量值的“发运”多维数据集；但是，该多维数据集中未包含盈利率的度量值。 通过在下列表达式中合并现有度量值，可以在多维数据集中创建一个计算成员来作为度量值，并将它命名为 Profit_per_Cubic_Meter：  
  
```  
([Measures].[Price_to_Ship] - [Measures].[Cost_to_Ship]) /  
[Measures].[Volume_in_Cubic_Meters]  
```  
  
 创建计算成员之后，下一次浏览“发运”多维数据集时，Profit_per_Cubic_Meter 将与其他度量值一起出现。  
  
 若要创建计算成员，请使用多维数据集设计器中的 "**计算**" 选项卡。 有关详细信息，请参阅[创建计算成员](../multidimensional-models/create-calculated-members.md)  
  
## <a name="named-sets"></a>命名集  
 命名集是返回集的 CREATE SET MDX 语句表达式。 MDX 表达式作为多维数据集定义的一部分保存在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 创建命名集的目的是为了重用多维表达式 (MDX) 查询。 使用命名集，业务用户可以简化查询，并针对复杂、常用的集表达式使用集名称而不是集表达式。 **相关主题：** [创建命名集](../multidimensional-models/create-named-sets.md)  
  
## <a name="script-commands"></a>脚本命令  
 脚本命令是一个 MDX 脚本，是多维数据集定义的一部分。 使用脚本命令，您可以执行几乎所有的受多维数据集的 MDX 支持的操作，例如，确定将计算仅应用于多维数据集的一部分的作用域。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，MDX 脚本可以应用于整个多维数据集，也可以应用于多维数据集的特定部分（在脚本执行过程中的特定点）。 默认脚本命令（CALCULATE 语句）会基于默认作用域使用聚合数据来填充多维数据集中的单元。  
  
 默认作用域为整个多维数据集，但是您可以定义更具限制的作用域（称为子多维数据集），然后将 MDX 脚本仅应用于该特定的多维数据集空间。 SCOPE 语句定义计算脚本中所有后续 MDX 表达式和语句的作用域，直到作用域终止或重新定义为止。 然后，使用 THIS 语句将 MDX 表达式应用于当前作用域。 可以使用 BACK_COLOR 语句为当前作用域中的单元指定背景单元颜色，以在调试期间提供帮助。  
  
 例如，您可以使用脚本命令并基于以前时间段销售额的加权值，跨时间和销售区域为雇员分配销售配额。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的计算](../multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
