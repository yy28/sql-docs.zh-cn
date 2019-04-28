---
title: 定义属性关系 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e49207e99887e13cdd5321821e7325b4a2dac7dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62717810"
---
# <a name="attribute-relationships---define"></a>特性关系 - 定义
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，属性是维度的基本构造块。 维度包含一组在属性关系基础上组织而成的属性。  
  
 对于维度中包含的每个表，都存在将表的键属性与该表的其他属性相关联的属性关系。 创建维度时可创建此关系。  
  
 属性关系具备以下优点：  
  
-   减少维度处理所需的内存量。 加快维度、分区和查询的处理速度。  
  
-   提高查询性能，因为存储访问速度更快而且执行计划更优化。  
  
-   如果用户定义的层次结构是沿关系路径定义的，则聚合设计算法会选择更有效的聚合。  
  
  
## <a name="attribute-relationship-considerations"></a>属性关系注意事项  
 当基础数据支持时，还应定义属性间唯一的属性关系。 若要定义唯一属性关系，请使用维度设计器的 **“属性关系”** 选项卡。  
  
 具有对外关系的任何属性必须具有与其相关属性关联的唯一键。 换言之，源属性中的一个成员必须并且只能标识相关属性中的一个成员。 例如，关系“City -> State”。 在此关系中，源属性为 City，相关属性为 State。 源属性为"多"方，并且在相关的端是多对一关系的"一"端。 源属性的键为 City + State。 有关详细信息，请参阅 [创建、修改或删除属性关系](../../analysis-services/multidimensional-models/attribute-relationships-create-modify-or-delete-relationship.md)  
  
 有关特性关系的属性详细信息，请参阅 [配置特性关系属性](../../analysis-services/multidimensional-models/attribute-relationships-configure-attribute-properties.md)。  
  
> [!NOTE]  
>  属性关系定义不正确会导致查询结果无效。  
  
## <a name="see-also"></a>请参阅  
 [中的维度设计器的](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  
