---
title: "内部成员属性 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: intrinsic member properties [MDX]
ms.assetid: 84e6fe64-9b37-4e79-bedf-ae02e80bfce8
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 823c8c1c387d2fb234fcf042cd416ce6e1ebb550
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-member-properties---intrinsic-member-properties"></a>MDX 成员属性的内部成员属性
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]公开内部属性，可以在查询返回其他数据或元数据用于在自定义应用程序，或以帮助进行模型调查或构造包含的维度成员。 如果您正在使用 SQL Server 客户端工具，可以在 SQL Server Management Studio (SSMS) 中查看内部属性。  
  
 内部属性包括 **ID**、 **KEY**、 **KEYx**和 **NAME**，这些是每个成员在任意级别公开的属性。 还可以返回位置信息，如 **LEVEL_NUMBER** 或 **PARENT_UNIQUE_NAME**等等。  
  
 根据您构造查询的方式和用于执行查询的客户端应用程序，成员属性在结果集中可能是可见的，也可能是不可见的。 如果您正在使用 SQL Server Management Studio 测试或运行查询，可以双击结果集中的某个成员以打开“成员属性”对话框，显示每个内部成员属性的值。  
  
 有关如何使用和查看维度成员属性的说明，请参阅 [在 SSMS 的“MDX 查询”窗口中查看 SSAS 成员属性](http://go.microsoft.com/fwlink/?LinkId=317362)。  
  
> [!NOTE]  
>  作为符合 1999 年 3 月发布的 OLE DB 规范 (2.6) OLAP 一节要求的提供程序， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持本主题中列出的内部成员属性。  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 以外的提供程序可能支持其他内部成员属性。 有关其他访问接口支持的内部成员属性的详细信息，请参阅这些访问接口附带的文档。  
  
## <a name="types-of-member-properties"></a>成员属性的类型  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持以下两种类型的内部成员属性：  
  
 上下文相关的成员属性  
 这些成员属性必须在特定层次结构或级别的上下文中使用，用于为指定维度或级别的每个成员提供值。  
  
 请注意以下示例如何包括 **KEY** 属性的路径： `MEMBER [Measures].[Parent Member Key] AS [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")`。  
  
 非上下文相关的成员属性  
 这些成员属性不能在特定维度或级别的上下文中使用，而是为某个轴上的所有成员返回值。  
  
 与上下文不相关的属性是独立的，不包括路径信息： 请注意，以下示例中没有为 **PARENT_UNIQUE_NAME** 指定任何维度或级别： `DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS`  
  
 不论内部成员属性是否是上下文相关的，都应遵循下列使用规则：  
  
-   只能指定与投影在轴上的维度成员相关的那些内部成员属性。  
  
-   可以在同一查询中同时包含对上下文相关成员属性和非上下文相关内部成员属性的请求。  
  
-   使用 **PROPERTIES** 关键字查询属性。  
  
 以下各节介绍了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中提供的各种上下文相关内部成员属性和非上下文相关内部成员属性，并介绍了如何将 **PROPERTIES** 关键字与每种类型的属性一起使用。  
  
## <a name="context-sensitive-member-properties"></a>上下文相关的成员属性  
 所有维度成员和级别成员都支持一列上下文相关的内部成员属性。 下表列出了这些上下文相关的属性。  
  
|“属性”|Description|  
|--------------|-----------------|  
|**ID**|在内部维护的成员 ID。|  
|**Key**|以原始数据类型表示的成员键的值。 MEMBER_KEY 用于向后兼容。  对于非组合键，MEMBER_KEY 具有与 KEY0 相同的值；对于组合键，MEMBER_KEY 属性为 null。|  
|**KEYx**|成员键，其中 x 是成员键的序号，起始值为零。 KEY0 适用于组合键和非组合键，但是主要用于组合键。<br /><br /> 对于组合键，KEY0、KEY1、KEY2 等共同构成了组合键。 您可以在查询中独立使用它们以返回组合键的该部分。 例如，指定 KEY0 返回组合键的第一部分，指定 KEY1 返回组合键的下一部分等等。<br /><br /> 如果键不是组合键，则 KEY0 与 **Key**等效。<br /><br /> 请注意， **KEYx** 可以在上下文中使用，也可以不带上下文使用。 因此，它显示在两个列表中。<br /><br /> 有关如何使用此成员属性的示例，请参阅 [简单的 MDX 小组件：Key0、Key1、Key2](http://go.microsoft.com/fwlink/?LinkId=317364)。|  
|**名称**|成员的名称。|  
  
### <a name="properties-syntax-for-context-sensitive-properties"></a>上下文相关属性的 PROPERTIES 语法  
 在特定维度或级别的上下文中使用这些成员属性，用于为指定维度或级别的每个成员提供值。  
  
 对于维度成员属性，在属性名称的前面加上属性适用的维度的名称。 下面的示例列出了正确的语法：  
  
 `DIMENSION PROPERTIES Dimension.Property_name`  
  
 对于级别成员属性，可以在属性名称的前面仅加上级别名称；或者，为了更加明确具体，也可以将维度名称和级别名称都加上。 下面的示例列出了正确的语法：  
  
 `DIMENSION PROPERTIES [Dimension.]Level.Property_name`  
  
 为了说明这一点，假设您希望返回 `[Sales]` 维度中引用的每个成员的所有名称。 若要返回这些名称，需要在多维表达式 (MDX) 查询中使用以下语句：  
  
 `DIMENSION PROPERTIES [Sales].Name`  
  
## <a name="non-context-sensitive-member-properties"></a>非上下文相关的成员属性  
 所有成员都支持一列内部成员属性，这些属性不因上下文而改变。 这些属性提供了一些附加信息，可供应用程序用来改善用户的体验。  
  
 下表列出了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持的非上下文相关的内部属性。  
  
> [!NOTE]  
>  MEMBERS 架构行集中的列支持下表中列出的内部成员属性。 有关 **MEMBERS** 架构行集的详细信息，请参阅 [MDSCHEMA_MEMBERS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)。  
  
|“属性”|Description|  
|--------------|-----------------|  
|**CATALOG_NAME**|此成员所属的多维数据集的名称。|  
|**CHILDREN_CARDINALITY**|成员具有的子级的个数。 它可以是一个估计值，所以不应依赖它进行确切计数。 访问接口应尽可能返回最精确的估计值。|  
|**CUSTOM_ROLLUP**|自定义成员表达式。|  
|**CUSTOM_ROLLUP_PROPERTIES**|自定义成员属性。|  
|**DESCRIPTION**|用户可以阅读的成员说明。|  
|**DIMENSION_UNIQUE_NAME**|此成员所属的维度的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**HIERARCHY_UNIQUE_NAME**|层次结构的唯一名称。 如果成员属于多个层次结构，则成员所属的每个层次结构都有对应的一行。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**IS_DATAMEMBER**|一个指示成员是否为数据成员的布尔值。|  
|**IS_PLACEHOLDERMEMBER**|用来指明成员是否为占位符的布尔值。|  
|**KEYx**|成员键，其中 x 是成员键的序号，起始值为零。 KEY0 可用于组合键和非组合键。<br /><br /> 如果键不是组合键，则 KEY0 与 **Key**等效。<br /><br /> 对于组合键，KEY0、KEY1、KEY2 等共同构成了组合键。 您可以在查询中独立引用它们以返回组合键的该部分。 例如，指定 KEY0 返回组合键的第一部分，指定 KEY1 返回组合键的下一部分等等。<br /><br /> 请注意， **KEYx** 可以在上下文中使用，也可以不带上下文使用。 因此，它显示在两个列表中。<br /><br /> 有关如何使用此成员属性的示例，请参阅 [简单的 MDX 小组件：Key0、Key1、Key2](http://go.microsoft.com/fwlink/?LinkId=317364)。|  
|**LCID** x|区域设置 ID 十六进制值中的成员标题的翻译，其中 *x* 是区域设置 ID 十进制值（例如，LCID1009 表示加拿大英语）。 这仅适用于翻译具有绑定到数据源的标题列的情况。|  
|**LEVEL_NUMBER**|成员距层次结构的根的距离。 根级别为零。|  
|**LEVEL_UNIQUE_NAME**|成员所属的级别的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**MEMBER_CAPTION**|与成员相关的标签或标题。 标题主要用于显示目的。 如果不存在标题，查询将返回 **MEMBER_NAME**。|  
|**MEMBER_KEY**|以原始数据类型表示的成员键的值。 MEMBER_KEY 用于向后兼容。  对于非组合键，MEMBER_KEY 具有与 KEY0 相同的值；对于组合键，MEMBER_KEY 属性为 null。|  
|**MEMBER_NAME**|成员的名称。|  
|**MEMBER_TYPE**|成员的类型。 此属性可以具有下列值之一：<br /><br /> **MDMEMBER_TYPE_REGULAR**<br /><br /> **MDMEMBER_TYPE_ALL**<br /><br /> **MDMEMBER_TYPE_FORMULA**<br /><br /> **MDMEMBER_TYPE_MEASURE**<br /><br /> **MDMEMBER_TYPE_UNKNOWN**<br /><br /> <br /><br /> 注意：MDMEMBER_TYPE_FORMULA 优先于 MDMEMBER_TYPE_MEASURE。 因此，如果 Measures 维度上有一个公式（计算）成员，则计算成员的 **MEMBER_TYPE** 属性为 MDMEMBER_TYPE_FORMULA。|  
|**MEMBER_UNIQUE_NAME**|成员的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**MEMBER_VALUE**|以原始类型表示的成员的值。|  
|**PARENT_COUNT**|此成员具有的父级的个数。|  
|**PARENT_LEVEL**|成员的父级距层次结构的根级别的距离。 根级别为零。|  
|**PARENT_UNIQUE_NAME**|成员的父成员的唯一名称。 对于根级别上的任何成员，均返回**NULL** 。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**SKIPPED_LEVELS**|跳过的成员级别数。|  
|**UNARY_OPERATOR**|成员的一元运算符。|  
|**UNIQUE_NAME**|成员的完全限定名称，它采用以下格式：[dimension].[level].[key6.]|  
  
### <a name="properties-syntax-for-non-context-sensitive-properties"></a>非上下文相关属性的 PROPERTIES 语法  
 使用以下语法指定使用 **PROPERTIES** 关键字的非上下文相关的内部成员属性：  
  
 `DIMENSION PROPERTIES Property`  
  
 请注意，此语法不允许使用维度或级别来限定属性。 因为非上下文相关的内部成员属性适用于某条轴上的所有成员，所以不能限定属性。  
  
 例如，指定 **DESCRIPTION** 内部成员属性的 MDX 语句具有以下语法：  
  
 `DIMENSION PROPERTIES DESCRIPTION`  
  
 此语句返回轴维度中各个成员的说明。 如果试图使用维度或级别限定属性，如在 *Dimension*`.DESCRIPTION` 或 *Level*`.DESCRIPTION`中，此语句将不会生效。  
  
### <a name="example"></a>示例  
 以下示例显示返回内部属性的 MDX 查询。  
  
 **示例 1：在查询中使用上下文相关的内部属性**  
  
 以下示例返回每个产品类别的父 ID、键和名称。 请注意属性如何公开为度量值。 这允许您在运行查询时在单元集中查看属性，而非在 SSMS 的“成员属性”对话框中查看。 您可能运行类似的查询以从部署的多维数据集检索成员元数据。  
  
```  
WITH  
MEMBER [Measures].[Parent Member ID] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("ID")  
MEMBER [Measures].[Parent Member Key] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")  
MEMBER [Measures].[Parent Member Name] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("Name")  
SELECT  
 {[Measures].[Parent Member ID], [Measures].[Parent Member Key], [Measures].[Parent Member Name] } on COLUMNS,   
 [Product].[Product Categories].AllMembers on ROWS  
FROM [Adventure Works]  
```  
  
 **示例 2：非上下文相关的内部属性**  
  
 以下示例是非上下文相关的内部属性的完整列表。 在 SSMS 中运行查询后，单击各个成员可以在“成员属性”对话框中查看属性。  
  
```  
SELECT [Measures].[Sales Amount Quota] on COLUMNS,  
[Employee].[Employees].members  
DIMENSION PROPERTIES  
 CATALOG_NAME ,   
 CHILDREN_CARDINALITY ,  
 CUSTOM_ROLLUP ,   
 CUSTOM_ROLLUP_PROPERTIES ,   
 DESCRIPTION ,   
 DIMENSION_UNIQUE_NAME ,   
 HIERARCHY_UNIQUE_NAME ,  
 IS_DATAMEMBER ,   
 IS_PLACEHOLDERMEMBER ,   
 KEY0 ,  
 LCID ,  
 LEVEL_NUMBER ,  
 LEVEL_UNIQUE_NAME ,  
 MEMBER_CAPTION ,   
 MEMBER_KEY ,   
 MEMBER_NAME ,   
 MEMBER_TYPE ,  
 MEMBER_UNIQUE_NAME ,   
 MEMBER_VALUE ,   
 PARENT_COUNT ,   
 PARENT_LEVEL ,   
 PARENT_UNIQUE_NAME ,  
 SKIPPED_LEVELS ,   
 UNARY_OPERATOR ,   
 UNIQUE_NAME    
 ON ROWS  
FROM [Adventure Works]  
WHERE [Employee].[Employee Department].[Department].&[Sales]  
```  
  
 **示例 3：将成员属性作为结果集中的数据返回**  
  
 下面的示例为指定区域设置的 Adventure Works 多维数据集中 Product 维度的产品类别成员返回翻译后的标题。  
  
```  
WITH   
MEMBER Measures.CategoryCaption AS Product.Category.CurrentMember.MEMBER_CAPTION  
MEMBER Measures.SpanishCategoryCaption AS Product.Category.CurrentMember.Properties("LCID3082")  
MEMBER Measures.FrenchCategoryCaption AS Product.Category.CurrentMember.Properties("LCID1036")  
SELECT   
{ Measures.CategoryCaption, Measures.SpanishCategoryCaption, Measures.FrenchCategoryCaption } ON 0  
,[Product].[Category].MEMBERS ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [PeriodsToDate (MDX)](../../../mdx/periodstodate-mdx.md)   
 [子级 &#40;MDX &#41;](../../../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX &#41;](../../../mdx/hierarchize-mdx.md)   
 [Count（集）(MDX)](../../../mdx/count-set-mdx.md)   
 [筛选器 &#40;MDX &#41;](../../../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX &#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX &#41;](../../../mdx/drilldownlevel-mdx.md)   
 [属性 &#40;MDX &#41;](../../../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX &#41;](../../../mdx/prevmember-mdx.md)   
 [使用成员属性 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [MDX 函数引用 &#40;MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
