---
title: 数据库维度属性 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7c7944ab279f2b036a3acd7cf75bd775d0ec6d6c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="database-dimension-properties"></a>数据库维度属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，由基于各种的维度属性的设置和上的属性或维度包含的层次结构的维度的元数据定义维度的特征。 下表说明了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的维度属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**AttributeAllMemberName**|指定维度中属性的“全部”成员的名称。|  
|**排序规则**|确定维度使用的排序规则。|  
|**CurrentStorageMode**|包含维度的当前存储模式。|  
|**DependsOnDimension**|包含维度所依赖的其他维度的 ID（如果有的话）。|  
|**Description**|包含维度的说明。|  
|**ErrorConfiguration**|可配置的错误处理设置，用于处理重复键、未知键、错误限制以及检测到错误执行的操作、错误日志文件和空键处理。|  
|**ID**|包含维度的唯一标识符 (ID)。|  
|**语言**|指定维度的默认语言。|  
|**MdxMissingMemberMode**|确定如何处理多维表达式 (MDX) 语句中缺少的成员。|  
|**MiningModelID**|包含数据挖掘维度所关联的挖掘模型的 ID。 此属性仅适用于挖掘模型维度。|  
|**名称**|指定维度的名称。|  
|**ProactiveCaching**|定义维度的主动缓存设置。|  
|**ProcessingGroup**|指定处理组。 值为 ByAttribute 或 ByTable。 默认值是**ByAttribute**。|  
|**ProcessingMode**|指示是否应该在处理期间或处理之后对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进行聚合以及为其建立索引。|  
|**ProcessingPriority**|确定在后台操作期间（例如惰性聚合、索引或群集）维度的处理优先级。|  
|**数据源**|标识维度绑定到的数据源视图。|  
|**StorageMode**|确定维度的存储模式。|  
|**类型**|指定维度的类型。|  
|**UnknownMember**|指示未知成员是否可见。|  
|**UnknownMemberName**|指定维度未知成员的标题，以维度的默认语言显示。|  
|**WriteEnabled**|指示维度写回是否可用（视安全权限而定）。|  
  
> [!NOTE]  
>  有关使用 null 值和其他数据完整性问题时设置值 ErrorConfiguration 和 UnknownMember 属性的详细信息，请参阅[中 Analysis Services 2005 中处理数据完整性问题](http://go.microsoft.com/fwlink/?LinkId=81891)。  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [维度关系](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [维度 & #40;Analysis Services-多维数据 & #41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
