---
title: 对属性成员 （离散化） 进行分组 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- NameColumn property
- discretization [Analysis Services]
- member groups [Analysis Services]
- grouping members
- DiscretizationNumber property
- sort orders [Analysis Services]
- DiscretizationMethod property
- adding members to member group
- number of member groups
- members [Analysis Services], groups
- names [Analysis Services], member groups
ms.assetid: 5cf2f407-accc-4baf-b54f-7703af338325
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e07f85d5a6162bed15393d8c255a55cf01b903c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251449"
---
# <a name="group-attribute-members-discretization"></a>对属性成员分组（离散化）
  成员组是系统生成的连续维度成员的集合。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，可以通过名为离散化的进程将属性成员分成若干成员组。 层次结构中的级别或者包含成员组，或者包含成员，但是不能同时包含二者。 业务用户浏览包含成员组的级别时，将看见成员组的名称和单元值。 由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 为了支持成员组而生成的成员称为分组成员，看上去与普通成员相同。  
  
 特性的 `DiscretizationMethod` 属性控制成员的分组方式。  
  
|`DiscretizationMethod` 设置|Description|  
|--------------------------------------|-----------------|  
|`None`|显示成员。|  
|`Automatic`|选择最佳数据表示的方法： 任一`EqualAreas`方法或`Clusters`方法。|  
|`EqualAreas`|尝试将属性中的成员分成若干包含相同数量成员的组。|  
|`Clusters`|尝试通过抽样定型数据、初始化为大量随机点和运行几次期望最大化 (EM) 聚类分析算法的迭代来将属性中的成员分成若干组。<br /><br /> 本方法的好处是适用于任何分布曲线，但就处理时间而言开销较大。|  
  
 特性的 `DiscretizationNumber` 属性指定要显示的组数。 如果将属性设置为默认值 0，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将通过对数据进行抽样或读取（具体取决于 `DiscretizationMethod` 属性的设置）来确定组数。  
  
 中的成员组的成员的排序顺序通过使用控制`OrderBy`特性的属性。 基于该排序顺序，成员组中的各成员将连续排列。  
  
 成员组的通常用法是从有很少成员的级别深化到有很多成员的级别。 若要允许用户在级别之间深化，请将包含大量成员的级别特性的 `DiscretizationMethod` 属性从 `None` 更改为上表中所述的离散化方法之一。 例如，“客户端”维度包含具有 500,000 个成员的“客户端名称”属性层次结构。 可以重命名该特性的客户端组和设置`DiscretizationMethod`属性设置为`Automatic`以显示特性层次结构成员级别成员组。  
  
 若要深化到每个组中的各个客户端，可以创建另一个绑定到相同表列的“客户端名称”属性层次结构。 然后根据两个属性创建新的用户层次结构。 顶级将基于“客户端组”属性，而较低级别基于“客户端名称”属性。 两个特性的 `IsAggregatable` 属性将为 `True`。 然后，用户可以展开层次结构上的“（所有）”级别以查看组成员，并展开组成员以查看层次结构的叶成员。 若要隐藏组或客户端级别，您可以将相应特性的 `AttributeHierarchyVisible` 属性设置为 `False`。  
  
## <a name="naming-template"></a>命名模板  
 当创建成员组时，会自动生成成员组的名称。 除非您指定了一个命名模板，否则使用默认的命名模板。 通过在某个特性的 `Format` 属性的 `NameColumn` 选项中指定命名模板，可以更改此命名方法。 可以针对列绑定（用于特性的 `Translations` 属性）的 `NameColumn` 集合中指定的每种语言重新定义不同的命名模板。  
  
 `Format` 设置使用以下字符串表达式来定义命名模板：  
  
 `<Naming template> ::= <First definition> [;<Intermediate definition>;<Last definition>]`  
  
 `<First definition> ::= <Name expression>`  
  
 `<Intermediate defintion> ::= <Name expression>`  
  
 `<Last definition> ::= <Name expression>`  
  
 `<First definition>` 参数只应用于第一个成员组或由离散化方法生成的成员组。 如果未提供可选参数 `<Intermediate definition>` 和 `<Last definition>` ，则 `<First definition>` 参数将用于为该属性生成的所有度量值组。  
  
 `<Last definition>` 参数只应用于由离散化方法生成的最后一个成员组。  
  
 `<Intermediate bucket name>` 参数应用于每个成员组，而不是由离散化方法生成的第一个或最后一个成员组。 如果生成的成员组仅为两个或更少，则忽略此参数。  
  
 `<Bucket name>` 参数是一个字符串表达式，可以合并一组变量以将成员或成员组信息表示为成员组名称的一部分：  
  
|变量|Description|  
|--------------|-----------------|  
|%{First bucket member}|包含在当前成员组中的第一个成员的名称。|  
|%{Last bucket member}|包含在当前成员组中的最后一个成员的名称。|  
|%{Previous bucket last member}|分配到上一个成员组的最后一个成员的名称。|  
|%{Next bucket first member}|分配到下一个成员组的第一个成员的名称。|  
|%{Bucket Min}|要分配到当前成员组的最小成员数。|  
|%{Bucket Max}|要分配到当前成员组的最大成员数。|  
|%{Previous Bucket Max}|要分配到上一个成员组的最大成员数。|  
|%{Next Bucket Min}|要分配到下一个成员组的最小成员数。|  
  
 为了与更早版本的 `"%{First bucket member} - %{Last bucket member}"`兼容，默认的命名模板为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
> [!NOTE]  
>  若要在命名模板中包含一个作为文字字符的分号 (;)，请在它前面加上一个百分号 (%) 字符。  
  
### <a name="example"></a>示例  
 以下字符串表达式可用于对 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 示例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中“客户”维度的“年收入”属性（其中，“年收入”属性使用了成员分组）进行分类：  
  
 "Less than %{Next Bucket Min};Between %{First bucket member} and %{Last bucket member};Greater than %{Previous Bucket Max}"  
  
## <a name="adding-new-members-to-existing-member-groups"></a>向现有的成员组中添加新成员  
 如果向维度中添加新成员，则这些成员便会通过比较成员值和当前成员组布局被分配到相应的成员组中。  
  
 如果在上一个成员组的最后一个成员和下一个成员组的第一个成员之间插入成员，则新成员便会成为上一个成员组的最后一个成员。  
  
## <a name="updating-a-dimension-with-discretized-attributes"></a>使用离散化属性更新维度  
 处理维度时，离散化属性只在完全更新 (ProcessFull) 中进行重新离散化。 若要对属性进行重新离散化，必须对维度执行完全更新。 如果离散化属性的维度表已更新，并且您使用增量式更新 (ProcessAdd) 处理该维度，则离散化属性不会进行重新离散化。 新存储桶的名称和子级将保持不变。 有关处理维度的详细信息，请参阅 [处理 Analysis Services 对象](processing-analysis-services-objects.md)。  
  
## <a name="usage-limitations"></a>使用限制  
  
-   不能在层次结构的最顶层或最底层中创建成员组。 如果您必须这样做，则可以添加一个级别，以使将在其中创建成员组的级别不再处于顶层或底层。 可以将级别的 `Visible` 属性设置为 `False` 来隐藏所添加的级别。  
  
-   不能在层次结构的两个连续级别中创建成员组。  
  
-   使用 ROLAP 存储模式的维度不支持成员组。  
  
-   如果成员组所在维度的维度表经过更新，并且该维度随后得到完全处理，则会生成一个新的成员组集。 新成员组的名称和子级可能与旧成员组的不同。  
  
## <a name="see-also"></a>请参阅  
 [属性和属性层次结构](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
