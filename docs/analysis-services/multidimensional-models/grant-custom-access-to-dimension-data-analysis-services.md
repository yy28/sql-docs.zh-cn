---
title: 授予对维度数据 (Analysis Services) 的自定义访问权限 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb93b4aeeaae9d659a225763286fc15a7d9f52a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208858"
---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>授予对维度数据的自定义访问权限 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  启用对多维数据集的读取访问权限后，可以设置明确允许或拒绝访问维度成员的其他权限（包括包含在度量值维度中的度量值，此维度包含在多维数据集中使用的全部度量值）。 例如，假设有多个经销商类别，您可能想要设置权限以排除某个具体业务类型的数据。 下图是拒绝访问“经销商”维度中“仓库”业务类型的前后对比效果。  
  
 ![数据透视表不包含维度成员与](../../analysis-services/multidimensional-models/media/ssas-permsdimdenied.png "数据透视表使用和不使用的维度成员")  
  
 默认情况下，如果可以读取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据集中的数据，则自动拥有对该多维数据集关联的所有度量值和维度成员的读取权限。 虽然这种行为可能足够应对许多方案，但有时安全要求需要一个更细化的授权策略，不同用户在同一维度的访问权限级别不同。  
  
 可通过选择允许 (AllowedSet) 或拒绝 (DeniedSet) 访问的成员来限制访问。 可通过选择或取消选择维度成员，从而使角色包括或去除所选成员来实现此目的。  
  
 基本维度安全性最容易；只需选择要在角色中包括或去除的维度属性和属性层次结构即可。 高级安全性更复杂，要求擅长 MDX 脚本编写。 下面将介绍这两种方法。  

> [!NOTE]  
>  以下说明假设有一个在 MDX 中发出查询的客户端连接。 如果该客户端使用 DAX（如 Power BI 中的 Power View），则维度安全性在查询结果中不明显。 有关详细信息，请参阅[了解用于多维模型的 Power View](understanding-power-view-for-multidimensional-models.md)。
      
## <a name="prerequisites"></a>先决条件  
 并非所有度量值或维度成员都可用于自定义访问方案。 如果某个角色限制访问默认度量值或成员，或者限制访问属于度量值表达式的度量值，则连接将失败。  
  
 **检查对维度安全性的阻碍：默认度量值、默认成员和度量值表达式中使用的度量值**  
  
1.  在 SQL Server Management Studio 中，右键单击多维数据集，然后选择**作为多维数据集脚本** | **ALTER To** | **新查询编辑器窗口**。  
  
2.  搜索 **DefaultMeasure**。 应发现一个针对多维数据集的度量值和一个针对每个透视的度量值。 定义维度安全性时，避免限制访问默认度量值。  
  
3.  然后，搜索 **MeasureExpression**。 度量值表达式是基于计算的度量值表达式，该计算通常包含其他度量值。 确认表达式中未使用要限制的度量值。 或者，继续操作并限制访问，只需确保在整个多维数据集内同样排除对该度量值的所有引用。  
  
4.  最后，搜索 **DefaultMember**。 请记录用作属性的默认成员的任何属性。 设置维度安全性时，避免对这些属性施加限制。  
  
## <a name="basic-dimension-security"></a>基本维度安全性  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，在对象资源管理器中展开相应数据库的“角色”  ，然后单击某个数据库角色（或创建一个新的数据库角色）。  
  
     此角色应已具有对多维数据集的读取访问权限。 如果需要此步骤的帮助信息，请参阅[授予多维数据集或模型权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。  
  
2.  在“维度数据”   | “基本”  上，选择要设置权限的维度。  
  
3.  选择属性层次结构。 并非所有属性都可用。 只有那些具有“AttributeHierarchyEnabled”  的属性才出现在  “属性层次结构”列表中。  
  
4.  选择要允许或拒绝访问的成员类型。 默认情况下，通过“选择所有成员”  选项允许访问。 建议保持此默认设置，然后清除通过此角色对“成员身份”  窗格中的 Windows 用户和组帐户不可见的个别成员。 这样做的好处在于，在未来处理操作中添加的新成员将自动对通过该角色进行连接的人员可用。  
  
     或者，你可以“取消选择所有成员”  以撤消所有访问权限，然后选择要允许的成员。 在未来处理操作中，新成员将不可见，直到手动编辑维度数据安全性以允许对其进行访问。  
  
5.  或者，单击“高级”  以启用该属性层次结构的“直观合计”  。 此选项根据通过该角色可用的成员重新计算聚合。  
  
    > [!NOTE]  
    >  应用剪裁维度成员的权限时，不会自动重新计算聚合合计。 假设在应用权限之前，属性层次结构的  “全部”成员返回一个值为 200 的计数。 应用拒绝访问某些成员的权限之后，即使对用户可见的成员值要少很多，  “全部”仍然会返回 200。 为了避免混淆多维数据集的使用者，可以将  “全部”成员配置为仅角色成员聚合，而非层次结构的所有成员聚合。 要调用此操作，可以在配置维度安全性时启用“高级” **Visual Totals** 选项卡上的  。 启用后，将在查询时间计算聚合，而不是从预先计算的聚合中检索。 这对查询性能有显著影响，因此仅在必要时使用。  
  
## <a name="hiding-measures"></a>隐藏度量值  
 在 [授予单元数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)中，已介绍了完全隐藏度量值的所有可视方面（不只其单元数据）要求具有对维度成员的权限。 本节将介绍如何拒绝访问度量值的对象元数据。  
  
1.  上**维度数据** | **基本**，向下的滚动维度列表直到到达多维数据集维度，然后选择**度量值维度**。  
  
2.  从度量值列表中，清除不应对通过该角色连接的用户显示的度量值复选框。  
  
> [!NOTE]  
>  检查先决条件，了解如何标识可能中断角色安全性的度量值。  
  
## <a name="advanced-dimension-security"></a>高级维度安全性  
 如果您具备 MDX 专业知识，另一种方法则是编写 MDX 表达式，设置允许或拒绝访问的成员的标准。 依次单击“创建角色”   | “维度数据”   | “高级”  来提供脚本。  
  
 可以使用 MDX 生成器编写 MDX 语句。 有关详细信息，请参阅 [MDX 生成器（Analysis Services -多维数据）](http://msdn.microsoft.com/library/fecbf093-65ea-4e1b-b637-f04876f1cb0f)。 **“高级”** 选项卡包含以下选项：  
  
 **Attribute**  
 选择要管理成员安全性的属性。  
  
 **允许的成员集**  
 AllowedSet 可以解析为“无成员”（默认）、“全部成员”或“部分成员”。 如果允许访问某个特性，但未定义允许集的成员，则授予对所有成员的权限。 如果允许访问属性并且定义了一组特定属性成员，则只有显式允许的成员才可见。  
  
 创建 AllowedSet 会在该属性加入多层层次结构时产生波纹效果。 例如，假设角色允许访问“华盛顿州”（假设这样一个场景：角色为公司华盛顿州销售部门授予权限）。 对于通过该角色连接的用户，包括上级（美国）或下级（西雅图和雷德蒙德）的查询将只能查看包括华盛顿州在内的链中的成员。 由于其他州未获得显式允许，因此效果将如同其被拒绝访问一样。  
  
> [!NOTE]  
>  如果定义了一个空集 ({}) 的属性成员的属性的任何成员都将对数据库角色可见。 缺少允许集不会被解释为空集。  
  
 **拒绝的成员集**  
 DeniedSet 属性可以解析为“无成员”、“全部成员”（默认）或“部分属性成员”。 当拒绝集只包含一组特定属性成员时，将仅对那些特定成员和下级（如果该属性位于多层层次结构中）拒绝访问数据库角色。 以华盛顿州销售部门为例。 如果“华盛顿”位于 DeniedSet，则通过该角色连接的用户可以看到除华盛顿及其下级属性以外的所有其他州。  
  
 回顾上一节可知，拒绝集是一个固定集合。 如果后续处理时引入了同样应被拒绝访问的新成员，则需编辑该角色，以将这些成员添加到列表。  
  
 **默认成员**  
 如果查询中未明确包含属性，DefaultMember 属性将确定返回到客户端的数据集。 如果未显式包含特性，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用特性的以下默认成员之一：  
  
-   如果数据库角色为特性定义了一个默认成员，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用该默认成员。  
  
-   如果数据库角色没有为特性定义默认成员，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用自己为该特性定义的默认成员。 除非另行指定，否则特性的默认成员为 **All** 成员（特性定义为不可聚合时除外）。  
  
 例如，假设数据库角色指定 **Male** 为 **Gender** 属性的默认成员。 除非查询在显式包含 **Gender** 特性的同时又为此特性指定了其他成员，否则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将返回仅包含男性客户的数据集。 有关设置默认成员的详细信息，请参阅 [定义默认成员](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)。  
  
 **启用直观合计**  
 VisualTotals 属性指示是根据所有单元值还是仅根据数据库角色可见的单元值来计算显示的聚合单元值。  
  
 默认情况下，禁用 VisualTotals 属性（设置为 **False**）。 此默认设置可以最大程度地利用性能，因为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以快速计算所有单元值的合计值，而不必花时间选择要计算的单元值。  
  
 但是，如果用户可以使用聚合集单元值来推导用户的数据库角色无权访问的特性成员的值，则禁用 VisualTotals 属性可能产生安全性问题。 例如， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用三个特性成员的值来计算一个聚合单元值。 数据库角色有权限查看这三个特性成员中的两个。 如果使用聚合单元值，此数据库角色的成员将能推导第三个特性成员的值。  
  
 将 VisualTotals 属性设置为 **True** 可以消除这种风险。 如果启用了 VisualTotals 属性，则数据库角色只能查看该角色有权访问的维度成员的聚合合计值。  
  
 **检查**  
 单击以测试此页面上定义的 MDX 语法。  
  
## <a name="see-also"></a>请参阅  
 [授予多维数据集或模型权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [授予单元数据的自定义访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)   
 [授予数据挖掘结构和模型的权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [授予数据源对象的权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
