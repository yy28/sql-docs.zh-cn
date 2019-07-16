---
title: CREATE SESSION CUBE 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ac95afcebcf07a5d691db5f2599b3290b9587d44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038358"
---
# <a name="mdx-data-definition---create-session-cube"></a>MDX 数据定义 - CREATE SESSION CUBE


  根据现有服务器多维数据集，创建和填充会话多维数据集。 会话多维数据集仅在当前会话内可见；不能从其他任何会话浏览或查询。 会话关闭时将隐式删除会话多维数据集。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE SESSION CUBE session_cube_name FROM <cube list> (<param list>)  
  
<cube list>::= source_cube_name [,<cube list>]  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= <reg dim from clause>   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN  
  
```  
  
## <a name="syntax-elements"></a>语法元素  
 session_cube_name  
 会话多维数据集的名称。  
  
 source_cube_name  
 会话多维数据集所基于的多维数据集的名称。  
  
 source_cube_name.measure_name  
 包含在会话多维数据集中的源度量值的完全限定名称。 不允许使用 Measures 维度的计算成员。  
  
 measure_name  
 会话多维数据集中的度量值的名称。  
  
 source_cube_name.dimension_name  
 包含在会话多维数据集中的源维度的完全限定名称。  
  
 dimension_name  
 会话多维数据集中的维度的名称。  
  
 从\<dim from 子句 >  
 该规范仅对于派生维度定义有效。  
  
 NOT_RELATED_TO_FACTS  
 该规范仅对于派生维度定义有效。  
  
 \<级别类型 >  
 该规范仅对于派生维度定义有效。  
  
## <a name="remarks"></a>备注  
 与服务器和本地多维数据集不同，会话多维数据集在创建该会话多维数据集的会话之外不会持久保留。 会话多维数据集按照定义它的度量值和定义来定义。 有两种类型的维度。  
  
-   源维度 - 这些维度是一个或多个源多维数据集的一部分。  
  
-   派生维度 - 这些维度能够提供新的分析功能。 派生维度可以是基于垂直或水平切片的源维度定义的常规维度，或者包含维度成员的自定义分组。 派生维度还可以是基于数据挖掘模型的数据挖掘维度。  
  
> [!NOTE]  
>  关键字“维度”可以指维度或层次结构。  
  
 会话多维数据集主要用于由客户端应用程序（如 Microsoft Excel）将属性成员动态分组到自定义成员组中。 在会话多维数据集中，可以执行下列任务：  
  
-   消除源多维数据集中存在的维度。  
  
-   从维度添加或消除层次结构。  
  
-   消除度量值组或特定度量值。  
  
-   基于属性绑定添加新属性，用于针对某个现有属性创建组。  
  
> [!IMPORTANT]  
>  会话多维数据集对象的安全性继承自基础源对象。 会话多维数据集还会继承其他对象，如操作和计算脚本。  
  
 CREATE SESSION CUBE 语句遵循下列规则：  
  
-   不能对父子层次结构执行分组。  
  
-   不能对 ROLAP 维度执行分组。  
  
-   不能对链接维度执行分组。  
  
-   不能对带有自定义汇总的级别执行分组。  
  
-   不能对离散化属性层次结构执行分组。  
  
-   不能对非自然层次结构执行分组，这些层次结构在各级之间存在多对多关系（如年龄和性别）。  
  
-   分组会中断对 MDX 脚本中的多维数据集名称的显式引用，因为会话多维数据集具有不同的名称。 请使用 CURRENTCUBE 关键字。  
  
-   不能对具有显式默认成员的维度执行分组。  
  
-   如果执行分组，则将删除原始服务器多维数据集中的会话作用域的计算成员。  
  
-   对服务器多维数据集中的某个多维数据集维度执行分组时，分组将影响基于同一维度的所有多维数据集维度。  
  
## <a name="example"></a>示例  
 以下示例说明如何创建 Adventure Works 多维数据集的会话作用域版本，该版本中包含 Reseller Sales Amount 度量值、Reseller 维度、Product 维度、Geography 维度和 Date 维度。 在此会话多维数据集内，将创建两个组；一个组包含欧洲各国家/地区，另一个组包含北美洲各国家/地区。 此示例是 CREATE SESSION CUBE 语句的简化版本，由 Microsoft Excel 在用户创建自定义成员分组时发出。  
  
```  
CREATE SESSION CUBE [Adventure Works_XL_GROUPING1]   
   FROM [Adventure Works]   
   ( MEASURE [Adventure Works].[Internet Sales Amount]  
   ,MEASURE [Adventure Works].[Reseller Sales Amount]  
   ,DIMENSION [Adventure Works].[Date].[Calendar]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Year]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Semester]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Quarter]  
   ,DIMENSION [Adventure Works].[Date].[Month Name]  
   ,DIMENSION [Adventure Works].[Date].[Date]  
   ,DIMENSION [Adventure Works].[Geography].[Country]   
      HIDDEN AS _XL_GROUPING81  
   ,DIMENSION [Adventure Works].[Geography].[State-Province]  
   ,DIMENSION [Adventure Works].[Geography].[City]  
   ,DIMENSION [Adventure Works].[Geography].[Postal Code]  
   ,DIMENSION [Adventure Works].[Geography].[Geography]  
   ,DIMENSION [Adventure Works].[Product].[Product Categories]  
   ,DIMENSION [Adventure Works].[Product].[Category]  
   ,DIMENSION [Adventure Works].[Product].[Subcategory]  
   ,DIMENSION [Adventure Works].[Product].[Product]  
   ,DIMENSION [Adventure Works].[Product].[Product Key]  
   ,DIMENSION [Adventure Works].[Reseller].[Reseller]  
   ,DIMENSION [Adventure Works].[Reseller].[Geography Key]  
   ,DIMENSION [Geography].[Country]   
      NOT_RELATED_TO_FACTS FROM _XL_GROUPING81   
          ( LEVEL [(All)]  
         ,LEVEL [Country1] GROUPING  
         ,LEVEL [Country]  
            ,GROUP [Country1].[CountryXl_Grp_1]   
                ( MEMBER [Geography].[Country].&[Canada]  
                  ,MEMBER [Geography].[Country].&[United States] )  
            ,GROUP [Country1].[CountryXl_Grp_2]   
                ( MEMBER [Geography].[Country].&[France]  
                  ,MEMBER [Geography].[Country].&[Germany]  
                  ,MEMBER [Geography].[Country].&[United Kingdom] )   
            )   
   )  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [CREATE GLOBAL CUBE 语句&#40;MDX&#41;](../mdx/mdx-data-definition-create-global-cube.md)  
  
  
