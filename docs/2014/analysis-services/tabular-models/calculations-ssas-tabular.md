---
title: 计算（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 738816e3-0e1d-44a5-8d1b-81068dce8ac0
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2da86ae5c5652c8b2614cae4bbb721802700d973
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939898"
---
# <a name="calculations-ssas-tabular"></a>计算（SSAS 表格）
  将数据导入模型之后，可以添加计算来聚合、筛选、扩展、组合和保护该数据。 表格模型采用数据分析表达式 (DAX)，这是一种用于创建自定义计算的公式语言。 在表格模型中，使用 DAX 公式创建的计算用在“计算列” **、“度量值” ** 和“行筛选器” ** 中。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[了解表格模型中的 DAX（SSAS 表格）](understanding-dax-in-tabular-models-ssas-tabular.md)|说明为表格模型中的计算列、度量值和行筛选器创建计算所用的数据分析表达式 (DAX) 公式语言。|  
|[DirectQuery 模式下的公式兼容性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|说明差异，列出在 DirectQuery 模式下不支持的函数，并列出受支持但可能返回不同结果的函数。|  
|[&#40;DAX&#41; 参考的数据分析表达式](/dax/data-analysis-expressions-dax-reference)|本节提供了 DAX 语法、运算符和函数的详细说明。|  
  
> [!NOTE]  
>  本节不提供用于创建计算的分步任务。 因为在计算列、度量值和行筛选器（在角色中）中指定了计算，在与这些功能相关的任务中将提供关于在何处创建 DAX 公式的说明。 有关详细信息，请参阅[创建计算列（SSAS 表格）](ssas-calculated-columns-create-a-calculated-column.md)、[创建和管理度量值（SSAS 表格）](measures-ssas-tabular.md)和[创建和管理角色（SSAS 表格）](roles-ssas-tabular.md)。  
  
> [!NOTE]  
>  尽管也可以使用 DAX 查询表格模型，但本节中的主题侧重于介绍如何使用 DAX 公式来创建计算。  
  
  
