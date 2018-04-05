---
title: 创建全局多维数据集语句 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GLOBAL CUBE
- CUBE
- GLOBAL
- CREATE
- CREATE GLOBAL
- CREATE GLOBAL CUBE
dev_langs:
- kbMDX
helpviewer_keywords:
- statements [MDX], CREATE GLOBAL CUBE
- CREATE GLOBAL CUBE
ms.assetid: b46f3c98-a4f1-4ebb-915f-a3333f4054dc
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 0e0dd4c6f3a5fe6fddf538389581f1554704691c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-definition---create-global-cube"></a>MDX 数据定义-创建全局多维数据集
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  基于服务器上某个多维数据集中的子多维数据集，创建并填充一个本地持久化多维数据集。 不需要连接到服务器就可以连接到本地持久化多维数据集。 有关本地多维数据集的详细信息，请参阅[本地多维数据集 &#40;Analysis Services-多维数据 &#41;](../analysis-services/multidimensional-models/olap-physical/local-cubes-analysis-services-multidimensional-data.md).  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE GLOBAL CUBE local_cube_name STORAGE 'Cube_Location'   
FROM source_cube_name (<param list>)  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= < dim DM from clause> | <reg dim from clause>   
  
<dim DM from clause>::= dm_model_name> COLUMN column_name   
  
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
 local_cube_name  
 本地多维数据集的名称。  
  
 'Cube_Location'  
 本地持久化多维数据集的名称和路径。  
  
 source_cube_name  
 本地多维数据集所基于的多维数据集的名称。  
  
 source_cube_name.measure_name  
 包含在本地多维数据集中的源度量值的完全限定名称。 不允许使用 Measures 维度的计算成员。  
  
 measure_name  
 本地多维数据集中的度量值的名称。  
  
 source_cube_name.dimension_name  
 包含在本地多维数据集中的源维度的完全限定名称。  
  
 dimension_name  
 本地多维数据集中的维度的名称。  
  
 从\<dim from 子句 >  
 该规范仅对于派生维度定义有效。  
  
 NOT_RELATED_TO_FACTS  
 该规范仅对于派生维度定义有效。  
  
 \<级别类型 >  
 该规范仅对于派生维度定义有效。  
  
## <a name="remarks"></a>Remarks  
 本地多维数据集是 definedin 使用条款的度量值和定义它的定义。 有两种类型的维度。  
  
-   源维度 - 这些维度是一个或多个源多维数据集的一部分  
  
-   派生维度 - 这些维度能够提供新的分析功能。 派生维度可以是基于垂直或水平切片的源维度定义的常规维度，或者包含维度成员的自定义分组。 派生维度还可以是基于数据挖掘模型的数据挖掘维度。  
  
> [!NOTE]  
>  关键字“维度”可以指维度或层次结构。  
  
 在本地多维数据集中，可以执行下列任务：  
  
-   消除源多维数据集中存在的维度  
  
-   从维度添加或消除层次结构  
  
-   消除度量值组或特定度量值  
  
 CREATE GLOBAL CUBE 语句遵循下列规则：  
  
-   CREATE GLOBAL CUBE 语句自动将所有命令（如计算度量值或操作）复制到本地多维数据集中。 如果某个命令包含显式引用父多维数据集的多维表达式 (MDX)，本地多维数据集将无法运行该命令。 若要防止出现此问题，请使用**CURRENTCUBE**关键字定义命令的 MDX 表达式时。 **CURRENTCUBE**关键字时引用在 MDX 表达式中的多维数据集，则使用当前的多维数据集上下文。  
  
-   对于从本地多维数据集文件中包含的现有全局多维数据集创建的全局多维数据集，不能将其保存到源本地多维数据集文件中。 例如，创建一个名为 SalesLocal1 的全局多维数据集并将其保存到 C:\SalesLocal.cub 文件中。 然后，连接到 C:\SalesLocal.cub 文件并创建第二个名为 SalesLocal2 的全局多维数据集。 现在，如果试图将 SalesLocal2 全局多维数据集保存到 C:\SalesLocal.cub 文件中，将收到一个错误。 但是，可以将 SalesLocal2 全局多维数据集保存到其他本地多维数据集文件中。  
  
-   全局多维数据集不支持非重复计数度量值。 因为包含非重复计数度量值的多维数据集是不可加的，所以 CREATE GLOBAL CUBE 语句不能支持创建或使用非重复计数度量值。  
  
-   向本地多维数据集添加度量值时，还必须至少包含一个与所添加度量值相关的维度。  
  
-   向本地多维数据集添加父子层次结构时，将忽略父子层次结构中的级别和筛选器，而将包括整个父子层次结构。  
  
-   本地多维数据集中不支持成员属性。  
  
-   无法基于透视创建本地多维数据集。  
  
-   向本地多维数据集中添加半累加性度量值时，以下规则适用：  
  
    -   如果所添加度量值的 AggregateFunction 属性是 ByAccount，则必须包含帐户维度。  
  
    -   如果所添加度量值的 AggregateFunction 属性是 FirstChild、LastChild、FirstNonEmpty、LastNonEmpty 或 AverageOfChildren，则必须包含整个时间维度。  
  
-   数据挖掘维度无法添加到本地多维数据集。  
  
-   引用维度被具体化并作为常规维度添加。  
  
-   包含多对多维度时，适用以下规则：  
  
    -   必须添加整个多对多维度。  
  
    -   必须添加中间度量值组。  
  
    -   必须添加通用于多对多关系中所涉及的两个度量值组的所有维度。  
  
 以下示例说明如何创建 Adventure Works 多维数据集的本地持久化版本，该版本只包含 Reseller Sales Amount 度量值、Reseller 维度和 Date 维度。  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller1.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
   )  
```  
  
 以下示例说明如何在创建本地多维数据集时进行切片。 所创建的全局多维数据集基于按 Fiscal Year 级别的 2005 成员垂直切片并按 Fiscal Year 和 Month 级别水平切片后的 Adventure Works 多维数据集。  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller2.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
      (  
LEVEL [Fiscal Year],  
LEVEL [Month],  
MEMBER [Date].[Fiscal].[Fiscal Year].&[2005]  
      )  
   )  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 数据定义语句 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [创建会话多维数据集语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-session-cube.md)  
  
  
