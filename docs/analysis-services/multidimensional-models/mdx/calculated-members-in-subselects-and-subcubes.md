---
title: "在嵌套 select 语句和子多维数据集中计算成员 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e35e8f7-ae1c-4549-8432-accf036d2373
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a2dc70e91783283b2b57fe6737c558375bb47f8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="calculated-members-in-subselects-and-subcubes"></a>嵌套 select 和子多维数据集中的计算成员
  计算成员是在运行时从表达式计算其值的维度成员，可用在嵌套 select 语句和子多维数据集中，以便更精确地定义查询的 cubespace。  
  
## <a name="enabling-calculated-members-in-the-subspace"></a>启用子空间中的计算成员  
 **子查询**中的连接字符串属性<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>或**DBPROPMSMDSUBQUERIES**中的属性[支持 XMLA 属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)在嵌套 select 语句中定义的行为或计算的成员或计算的集的宽限期或子多维数据集。 在本文档的上下文中，如果没有特别指明，则嵌套 select 表示嵌套 select 和子多维数据集。  
  
 SubQueries 属性允许以下值。  
  
|||  
|-|-|  
|“值”|说明|  
|0|计算成员不允许在嵌套 select 或子多维数据集中使用。<br /><br /> 如果引用计算成员，则在对嵌套 select 或子多维数据集进行计算时，将引发错误。|  
|1|计算成员允许在嵌套 select 或子多维数据集中使用，但在返回子空间中不引入祖先成员。|  
|2|计算成员允许在嵌套 select 或子多维数据集中使用，并且在返回子空间中引入祖先成员。 此外，在选择计算成员时允许使用混合粒度。|  
  
 在 SubQueries 属性中使用值 1 或 2 允许计算成员用于筛选嵌套 select 的返回子空间。  
  
 将通过一个例子帮助阐明这个概念；首先，必须创建一个计算成员，然后发出一个嵌套 select 查询以便说明上述行为。  
  
 下面的示例创建一个计算成员，该计算成员将 [Seattle Metro] 作为城市添加到 Washington 州下的 [Geography].[Geography] 层次结构中。  
  
 为了运行该示例，连接字符串必须包含具有值 1 的 SubQueries 属性，并且所有 MDX 语句必须在同一会话中运行。  
  
> [!IMPORTANT]  
>  如果正使用 Management Studio 来测试查询，请单击连接管理器上的“选项”按钮访问其他连接字符串属性窗格，你可以在其中输入 subqueries = 1 或 2，以允许子空间中的计算成员。  
  
 首先发出以下 MDX 表达式：  
  
```  
  
CREATE MEMBER [Adventure Works].[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]   
   AS  AGGREGATE(   
                 {   
                   [Geography].[Geography].[City].&[Bellevue]&[WA]  
                 , [Geography].[Geography].[City].&[Issaquah]&[WA]  
                 , [Geography].[Geography].[City].&[Redmond]&[WA]  
                 , [Geography].[Geography].[City].&[Seattle]&[WA]  
                 }  
                )    
```  
  
 然后发出以下 MDX 查询以便查看在嵌套 select 中允许的计算成员。  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]} on 0 from [Adventure Works])  
Where [Measures].[Reseller Sales Amount]  
```  
  
 获得的结果如下：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2011|CY 2012|CY 2013|CY 2014|  
|Seattle Metro Agg|$2,383,545.69|1$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 如前所述，在 SubQueries=1 时，[Seattle Metro] 的祖先在返回的子空间中不存在，因此，[Geography].[Geography].allmembers 仅包含计算成员。  
  
 如果使用 SubQueries=2 运行该示例，则在连接字符串中，获得的结果如下：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|(null)|(null)|(null)|(null)|(null)|  
|United States|(null)|(null)|(null)|(null)|(null)|  
|Washington|(null)|(null)|(null)|(null)|(null)|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 如前所述，在使用 SubQueries=2 时，[Seattle Metro] 的祖先存在于返回的子空间中，但对于这些成员不存在任何值，因为没有要为聚合提供的常规成员。 因此，在此示例中，为计算成员的所有祖先成员提供 NULL 值。  
  
 为了理解上述行为，您需要了解的是：与常规成员不同，计算成员并不影响其父级的聚合；这意味着单独按计算成员进行筛选将导致空的祖先，因为没有常规成员影响最终生成的子空间的聚合值。 如果您将常规成员添加到筛选表达式，则聚合值将来自这些常规成员。 继续以上面的示例为例，如果 Oregon 州的 Portland 市以及 Washington 州的 Spokane 市添加到计算成员出现的同一轴中；如下一个 MDX 表达式所示：  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {  
               [Seattle Metro Agg]  
             , [Geography].[Geography].[City].&[Portland]&[OR]  
             , [Geography].[Geography].[City].&[Spokane]&[WA]  
             } on 0 from [Adventure Works]  
     )  
Where [Measures].[Reseller Sales Amount]  
```  
  
 将获得以下结果。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|United States|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|Oregon|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Portland|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|97205|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Washington|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Spokane|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|99202|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 在上面的结果中，[All Geographies]、[United States]、[Oregon] 和 [Washington] 的聚合值来自对 &[Portland]&[OR] 和 &[Spokane]&[WA] 的后代执行的聚合。 没有任何内容来自计算成员。  
  
### <a name="remarks"></a>注释  
 在嵌套 select 或子多维数据集表达式中只允许全局或会话计算成员。 在对嵌套 select 或子多维数据集表达式执行计算时，如果在 MDX 表达式中具有查询计算成员，将引发错误。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [在查询中的嵌套 select 语句](../../../analysis-services/multidimensional-models/mdx/subselects-in-queries.md)   
 [支持的 XMLA 属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)  
  
  
