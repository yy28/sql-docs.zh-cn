---
title: 父-子层次结构 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], parent-child
- dimensions [Analysis Services], parent-child
- parent attributes [Analysis Services]
- data members [Analysis Services]
- hierarchies [Analysis Services], multilevel
- self-joins
- self-referencing relationships
- members [Analysis Services], data
- parent-child dimensions [Analysis Services]
ms.assetid: 4657f5dc-d88e-48d2-a448-08f79bc89546
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be08164b3e96f5995c5ed1b64edc83699c7d8b40
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505565"
---
# <a name="parent-child-hierarchy"></a>父-子层次结构
  父子层次结构是标准维度中包含父属性的层次结构。 父属性用于说明维度主表内部的自引用关系或自联接。 父子层次结构是根据单个父属性构造的。 层次结构中出现的级别是通过与父属性关联的成员之间的父子关系形成的，因此只为一个父子层次结构分配一个级别。 父子层次结构内成员的位置由父特性的 `KeyColumns` 和 `RootMemberIf` 属性确定，而级别内成员的位置则由父特性的 `OrderBy` 属性确定。 有关特性属性的详细信息，请参阅 [属性和属性层次结构](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)。  
  
 由于父子层次结构中各级别之间均存在父子关系，因此一些非叶成员除了包含从子成员聚合的数据外，还可以包含派生自基础数据源的数据。  
  
## <a name="dimension-schema"></a>维度架构  
 父子层次结构的维度架构依赖于维度主表中提供的自引用关系。 例如，以下关系图说明了 **示例数据库中的** DimOrganization [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 维度主表。  
  
 ![DimOrganization 表中的自引用联接](../dev-guide/media/dimorganization.gif "DimOrganization 表中的自引用联接")  
  
 在该维度表中， **ParentOrganizationKey** 列与 **OrganizationKey** 主键列具有外键关系。 换言之，该表中的每个记录都可以通过父子关系与该表中的其他记录相关联。 这种自联接通常用于表示单位的实体数据，例如某个部门内部的雇员管理结构。  
  
## <a name="hierarchies-and-levels"></a>层次结构和级别  
 不具有父子关系的维度通过分组依据属性和排序依据属性来构造层次结构。 这些维度从属性名称中派生出其层次结构的级别名称。  
  
 但是，父子维度通过检查维度主表中包含的数据，然后评估该表中记录之间的父子关系来构造父子层次结构。 有关父子层次结构的详细信息，请参阅 [用户层次结构](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)。  
  
 父子层次结构不会从用于创建层次结构的属性中派生父子层次结构中级别的名称。 相反，这些维度创建级别名称会自动使用的命名模板的字符串表达式可以指定控制属性如何生成属性层次结构的父属性的级别。 有关如何设置父属性的命名模板的详细信息，请参阅 [属性和属性层次结构](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)。  
  
## <a name="data-members"></a>数据成员  
 通常，维度中的叶成员包含直接派生自基础数据源的数据，而非叶成员包含派生自对子成员所执行的聚合的数据。  
  
 但是在父子层次结构中，一些非叶成员除了包含基于子成员聚合的数据外，还可能包含派生自基础数据源的数据。 对于父子层次结构中的这些非叶成员，可为其创建包含基础事实数据表数据的特殊的系统生成子成员。 这些特殊子成员称为“数据成员 ”，它们包含一个与非叶成员直接相关、且与通过该非叶成员后代计算出来的汇总值无关的值。 有关数据成员的详细信息，请参阅[父子层次结构中的属性](parent-child-dimension-attributes.md)。  
  
## <a name="see-also"></a>请参阅  
 [父子层次结构中的属性](parent-child-dimension-attributes.md)   
 [数据库维度属性](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)  
  
  
