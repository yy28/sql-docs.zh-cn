---
title: "查询多维数据使用 MDX |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multidimensional data [Analysis Services], querying
ms.assetid: e0a5dd60-35a3-4a4f-b36f-52ecea814886
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6a5e30c527a170b533b61033b27b08cd780b6fd7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="querying-multidimensional-data-with-mdx"></a>使用 MDX 查询多维数据
  多维表达式 (MDX) 是用于在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中处理和检索多维数据的查询语言。 MDX 基于 XML for Analysis (XMLA) 规范，并带有特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]的扩展。 MDX 使用由标识符、值、语句、函数和运算符组成的表达式， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 可以通过计算表达式来检索某个对象（如集或成员）或标量值（如字符串或数字）。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的 MDX 查询和表达式可用于执行以下操作：  
  
-   从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 多维数据集向客户端应用程序返回数据。  
  
-   设置查询结果的格式。  
  
-   执行多维数据集设计任务，包括定义计算成员、命名集、范围分配和关键绩效指标 (KPI)。  
  
-   执行管理任务，包括维度和单元安全性。  
  
 MDX 在很多方面与关系数据库常用的 SQL 语法看起来很相似。 但是，MDX 并非 SQL 语言的扩展，在许多方面都有别于 SQL。 为了创建用于设计或保护多维数据集的 MDX 表达式，或创建 MDX 查询以返回多维数据并设置其格式，您需要了解有关 MDX 和维度建模的基本概念、MDX 语法元素、MDX 运算符、MDX 语句以及 MDX 函数。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[MDX 中的重要概念 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)|可以使用多维表达式 (MDX) 查询多维数据或创建多维数据集中使用的 MDX 表达式，但是应先了解 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 维度的概念和术语。|  
|[MDX 查询基础知识 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)|多维表达式 (MDX) 使您可以查询多维对象（如多维数据集）并返回包含该多维数据集的数据的多维单元集。 本主题及其子主题提供 MDX 查询的概述。|  
|[MDX 脚本编写基础知识 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，多维表达式 (MDX) 脚本由一个或多个 MDX 表达式或语句构成，这些表达式或语句使用计算结果填充多维数据集。<br /><br /> MDX 脚本定义多维数据集的计算过程。 MDX 脚本也被视为多维数据集的一部分。 因此，更改与多维数据集相关联的 MDX 脚本将会立即更改多维数据集的计算过程。<br /><br /> 要创建 MDX 脚本，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的“多维数据集设计器”。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 语法元素 (MDX)](../../../mdx/mdx-syntax-elements-mdx.md)   
 [MDX 语言参考 (MDX)](../../../mdx/mdx-language-reference-mdx.md)  
  
  

