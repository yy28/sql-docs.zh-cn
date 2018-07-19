---
title: 计算 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f2f137312af7b4ef7d77334b3830cd337a849f42
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983919"
---
# <a name="calculations"></a>“新建命名集” 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  将数据导入模型之后，可以添加计算来聚合、筛选、扩展、组合和保护该数据。 表格模型采用数据分析表达式 (DAX)，这是一种用于创建自定义计算的公式语言。 在表格模型中，使用 DAX 公式创建的计算用在“计算列” 、“度量值” 和“行筛选器” 中。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[了解表格模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|说明为表格模型中的计算列、度量值和行筛选器创建计算所用的数据分析表达式 (DAX) 公式语言。|  
|[在 DirectQuery 模式下的 DAX 公式兼容性](http://msdn.microsoft.com/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|说明差异，列出在 DirectQuery 模式下不支持的函数，并列出受支持但可能返回不同结果的函数。|  
|[数据分析表达式 (DAX) 参考](http://msdn.microsoft.com/70a82136-0926-4a91-bcb3-e18e82593b0d)|本节提供了 DAX 语法、运算符和函数的详细说明。|  
  
> [!NOTE]  
>  本节不提供用于创建计算的分步任务。 因为在计算列、度量值和行筛选器（在角色中）中指定了计算，在与这些功能相关的任务中将提供关于在何处创建 DAX 公式的说明。 有关详细信息，请参阅[创建计算列](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)，[创建和管理度量值](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)，并[创建和管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
> [!NOTE]  
>  尽管也可以使用 DAX 查询表格模型，但本节中的主题侧重于介绍如何使用 DAX 公式来创建计算。  
  
  
