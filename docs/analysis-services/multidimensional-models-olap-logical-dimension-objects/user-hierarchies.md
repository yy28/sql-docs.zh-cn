---
title: "用户层次结构 |Microsoft 文档"
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
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- members [Analysis Services], hierarchies
- dimensions [Analysis Services], hierarchies
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], hierarchies
- parent-child hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
- ragged hierarchies [Analysis Services]
- balanced hierarchies [Analysis Services]
- hierarchies [Analysis Services]
- OLAP objects [Analysis Services], hierarchies
- multilevel hierarchies [Analysis Services]
- unbalanced hierarchies [Analysis Services]
ms.assetid: 9394e9a3-2242-4f0e-85e0-25d499d2d3b6
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 069f68e31f516a7f90a07cd462b70e0b455ab800
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="user-hierarchies"></a>用户层次结构
  用户定义层次结构是用户定义的层次结构中使用的特性[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]将维度的成员组织为分层结构并提供多维数据集中的导航路径。 例如，下表定义了时间维度的维度表。 维度表支持三个属性，即年份、季度和月份。  
  
|Year|季度|Month|  
|----------|-------------|-----------|  
|1999|季度 1|一月|  
|1999|季度 1|二月|  
|1999|季度 1|三月|  
|1999|季度 2|四月|  
|1999|季度 2|五月|  
|1999|季度 2|六月|  
|1999|第 3 季度|七月|  
|1999|第 3 季度|八月|  
|1999|第 3 季度|九月|  
|1999|第四季度|Oct|  
|1999|第四季度|十一月|  
|1999|第四季度|Dec|  
  
 用年份、季度和月份属性来构造时间维度中由用户定义的层次结构（即日历）。 “日历”维度（常规维度）的级别和成员之间的关系如下面的关系图所示：  
  
 ![时间维度的级别和成员的层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/as-levelconcepts.gif "时间维度的级别和成员的层次结构")  
  
> [!NOTE]  
>  默认的二级属性层次结构除外的其他任何层次结构都称为用户定义层次结构。 有关属性层次结构的详细信息，请参阅[属性和属性层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)。  
  
## <a name="member-structures"></a>成员结构  
 除父子层次结构以外，成员在层次结构中的位置由属性在层次结构定义中的顺序进行控制。 层次结构定义中的每个属性均构成层次结构中的一个级别。 成员在级别中的位置由用于创建该级别的属性的顺序来确定。 用户定义层次结构的成员结构可以占用四个基本窗体中的某一个，具体取决于成员之间的相互关系。  
  
### <a name="balanced-hierarchies"></a>均衡层次结构  
 在均衡层次结构中，层次结构的所有分支降至相同的级别，并且每个成员的逻辑父级直接位于该成员的上一级别。 在 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 示例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中，“产品”维度的“产品类别”层次结构就是一个均衡层次结构的示例。 “产品名称”级别的每个成员均在“子类别”级别中有一个父成员，而每个“子类别”级别在“类别”级别中也有一个父成员。 而且，层次结构中的每个分支在“产品名称”级别中都有叶成员。  
  
### <a name="unbalanced-hierarchies"></a>不均衡层次结构  
 在不均衡层次结构中，层次结构的分支降至不同级别。 父子层次结构是不均衡层次结构。 例如，[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 示例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的“组织”维度包含了表示每个雇员的成员。 CEO 是层次结构中的顶级成员，而部门经理和执行秘书直接位于 CEO 下面。 部门经理还有下属成员，但执行秘书没有。  
  
 最终用户可能无法区别不均衡层次结构和不规则层次结构。 但可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的不同技术和属性来支持这两种层次结构类型。 有关详细信息，请参阅[不规则层次结构](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)，和[父-子层次结构中的特性](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)。  
  
### <a name="ragged-hierarchies"></a>不规则层次结构  
 在不规则层次结构中，至少一个成员的逻辑父成员不直接位于该成员的上一级。 这将导致层次结构的分支降至不同的级别。 例如，用洲、国家（地区） 和市县级别定义的“地域”维度中，各成员将按定义顺序显示，成员 Europe 显示在层次结构的顶层，成员 France 显示在中层，而成员 Paris 显示在底层。 France 比 Europe 更具体，而 Paris 比 France 更具体。 对此常规层次结构进行以下更改：  
  
-   将 Vatican City 成员添加到国家（地区）级别。  
  
-   向市县级别添加成员并将这些成员与国家（地区）级别中的 Vatican City 成员建立关联。  
  
-   将省市自治区级别添加到国家（地区）级别和市县级别之间。  
  
 将与国家（地区）级别中的其他成员关联的成员填入省市自治区级别中，将市县级别中的成员与省市自治区级别中相应的成员建立关联。 但是，由于国家（地区）级别的 Vatican City 成员在省市自治区级别中没有相关联的成员，所以必须将市县级别的成员直接关联到国家（地区）级别的 Vatican City 成员。 因为这些更改，该维度的层次结构现在成为不规则层次结构。 城市 Vatican City 的父级是国家/地区 Vatican City，而它并不直接位于市县级别的 Vatican City 成员的上一级。 有关详细信息，请参阅 [不规则层次结构](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)。  
  
### <a name="parent-child-hierarchies"></a>父子层次结构  
 维度的父子层次结构是通过使用特殊属性（称为父属性）来定义的，目的是为了确定成员之间的相互关系。 父属性用于说明维度主表内部的自引用关系或自联接。 父子层次结构是根据单个父属性构造的。 层次结构中出现的级别是通过与父属性关联的成员之间的父子关系形成的，因此只为一个父子层次结构分配一个级别。 父子层次结构的维度架构依赖于维度主表中提供的自引用关系。 例如下, 图说明**DimOrganization**维度主表中的[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]示例数据库。  
  
 ![DimOrganization 表中的自引用联接](../../analysis-services/multidimensional-models/media/dimorganization.gif "DimOrganization 表中的自引用联接")  
  
 在该维度表中， **ParentOrganizationKey** 列与 **OrganizationKey** 主键列具有外键关系。 换言之，该表中的每个记录都可以通过父子关系与该表中的其他记录相关联。 这种自联接通常用于表示单位的实体数据，例如某个部门内部的雇员管理结构。  
  
 创建父子层次结构时，两个属性所表示的列都必须有相同的数据类型。 两个属性还必须在同一个表中。 默认情况下，任何成员的父键只要等于其自身的成员键、空、0（零）或一个未出现在成员键列中的值，则该成员将被认为是顶层中的成员（不包括“（全部）”级别）。  
  
 父子层次结构的深度可以在其层次结构分支中变化。 换句话说，父子层次结构被视为非平衡层次结构。  
  
 在用户定义层次结构中，层次结构的级别数决定着最终用户所能看见的级别数，而与用户定义层次结构不同，父子层次结构是使用单个级别的属性层次结构定义的，并且此单个级别中的值将生成用户所能看见的多个级别。 存储成员键和父键的维度表列的内容将决定显示出的级别数目。 如果维度表中的数据发生更改，则级别数也会更改。 有关详细信息，请参阅[父-子维度](../../analysis-services/multidimensional-models/parent-child-dimension.md)，和[父-子层次结构中的特性](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建用户定义层次结构](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [用户层次结构属性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [维度特性属性参考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
