---
title: Autoexists |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 56283497-624c-45b5-8a0d-036b0e331d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc9aa519d37b040026414ab826373357a1ddd92f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074731"
---
# <a name="autoexists"></a>Autoexists
  “autoexists” ** 的概念将多维数据集空间限制为在多维数据集中实际存在的那些单元，而不是可能由于从同一层次结构创建属性层次结构成员的所有可能组合而存在的那些单元。 其原因在于，一个属性层次结构的成员不能与同一维度中其他属性层次结构的成员共存。 在 SELECT 语句中使用同一维度的两个或更多属性层次结构时，Analysis Services 会计算这些属性的表达式，以确保这些属性的成员得到适当限制，使它们满足所有其他属性的条件。  
  
 例如，假定您在处理来自 Geography 维度的属性。 如果您有一个表达式返回 City 属性中的所有成员，另一个表达式将 Country 属性中的成员限定为欧洲的所有国家/地区，这样将使 City 成员限制为仅属于欧洲国家的城市。 其原因就在于 Analysis Services 的 autoexists 特性。 Autoexists 仅适用于同一维度中的属性，因为它试图阻止在一个属性表达式中排除的维度记录被包括在其他属性表达式中。 也可以将 Autoexists 理解为不同的属性表达式产生的维度行的交集。  
  
## <a name="cell-existence"></a>单元存在性  
 以下单元始终存在：  
  
-   在与同一维度中其他层次结构的成员相交时，每个层次结构的“（全部）”成员。  
  
-   在与其非计算同级相交或者与其非计算同级的父级或子级相交时的计算成员。  
  
## <a name="providing-non-existing-cells"></a>提供不存在的单元  
 不存在的单元是系统为响应请求在多维数据集中不存在的单元的查询或计算而提供的单元。 例如，如果某多维数据集具有 City 属性层次结构、属于 Geography 维度的 Country 属性层次结构和 Internet Sales Amount 度量值，则此多维数据集的空间仅包含那些共存的成员。 例如，如果 City 属性层次结构包含城市 New York、London、Paris、Tokyo 和 Melbourne，而 Country 属性层次结构包含国家（地区）United States、United Kingdom、France、Japan 和 Australia，则该多维数据集的空间不包含 Paris 和 United States 相交处的空间（单元）。  
  
 当查询单元不存在时，不存在的单元返回空，即它们无法包含计算结果，并且您不能定义写入此空间的计算。 例如，下面的语句包含不存在的单元。  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  此查询使用 [Members (Set) (MDX)](/sql/mdx/members-set-mdx) 函数返回列轴上 Gender 属性层次结构的成员集，并将此集与行轴上 Customer 属性层次结构的指定成员集相交。  
  
 执行前面的查询时，Aaron A. Allen 与 Female 相交处的单元将显示空。 同样，Abigail Clark 与 Male 相交处的单元也将显示空。 这些单元不存在并且不能包含值，但不存在的单元可出现在查询返回的结果中。  
  
 如果使用 [Crossjoin (MDX)](/sql/mdx/crossjoin-mdx) 函数返回同一维度中属性层次结构中的属性层次结构成员的叉积，自动共存将限制只返回那些实际存在的元组集，而不是返回整个笛卡尔乘积的元组。 例如，运行以下查询并检查其结果。  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  请注意 0 用于表示列轴的名称，它是列轴“axis(0)”的简称。  
  
 前面的查询仅为查询中每个属性层次结构的共存成员返回单元。 前面的查询还可以使用[交叉结合（MDX）](/sql/mdx/crossjoin-mdx)函数的新 * 变体来编写。  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 前面的查询还可以通过以下方式来编写：  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 虽然结果集中的元数据将不同，但返回的单元值将是相同的。 例如，在前面的查询中，Country 层次结构已移到切片器轴（在 WHERE 子句中），因此没有显式显示在结果集中。  
  
 这三个前面的查询都说明了中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]的自动共存行为的影响。  
  
## <a name="deep-and-shallow-autoexists"></a>深度和浅表 Autoexists  
 Autoexists 可以深度或浅表的形式应用于表达式。 
  `Deep Autoexists` 意味着将对所有表达式进行计算，以便在应用了切片器表达式、轴中的嵌套 select 表达式等后到达可能的最深空间。 
  `Shallow Autoexists` 意味着在将当前表达式和这些结果传递到当前表达式之前对外部表达式进行计算。 默认设置为深度 autoexists。  
  
 下面的应用场景和示例将帮助阐明不同类型的 Autoexists。 在下面的示例中，将创建两个集：一个作为计算表达式，另一个作为常量表达式。  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 获得的结果集如下：  
  
|||||  
|-|-|-|-|  
||**分销商销售额**|**Discount Amount**|**PCT 折扣**|  
|**山地-200**|**$14356699.36**|**$19012.71**|**0.13%**|  
|**道路-250**|**$9377457.68**|**$4032.47**|**0.04%**|  
|**山地-100**|**$8568958.27**|**$139393.27**|**1.63%**|  
|**道路-650**|**$7442141.81**|**$39698.30**|**0.53%**|  
|**旅行-1000**|**$6723794.29**|**$166144.17**|**2.47%**|  
|**公路-550-W**|**$3668383.88**|**$1901.97**|**0.05%**|  
|**公路-350-W**|**$3665932.31**|**$20946.50**|**0.57%**|  
|**HL 山地框**|**$3365069.27**|**$174.11**|**0.01%**|  
|**道路-150**|**$2363805.16**|**$0.00**|**0.00%**|  
|**旅行-3000**|**$2046508.26**|**$79582.15**|**3.89%**|  
  
 获得的产品集似乎与 Preferred10Products 相同；因此，请验证 Preferred10Products 集：  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 根据以下结果，两个产品集（Top10SellingProducts 和 Preferred10Products）是相同的  
  
|||||  
|-|-|-|-|  
||**分销商销售额**|**Discount Amount**|**PCT 折扣**|  
|**山地-200**|**$14356699.36**|**$19012.71**|**0.13%**|  
|**道路-250**|**$9377457.68**|**$4032.47**|**0.04%**|  
|**山地-100**|**$8568958.27**|**$139393.27**|**1.63%**|  
|**道路-650**|**$7442141.81**|**$39698.30**|**0.53%**|  
|**旅行-1000**|**$6723794.29**|**$166144.17**|**2.47%**|  
|**公路-550-W**|**$3668383.88**|**$1901.97**|**0.05%**|  
|**公路-350-W**|**$3665932.31**|**$20946.50**|**0.57%**|  
|**HL 山地框**|**$3365069.27**|**$174.11**|**0.01%**|  
|**道路-150**|**$2363805.16**|**$0.00**|**0.00%**|  
|**旅行-3000**|**$2046508.26**|**$79582.15**|**3.89%**|  
  
 下面的示例将阐释深度 Autoexists 的概念。 在该示例中，我们将依据 [Product].[Product Line] 属性对 [Mountain] 组中的产品筛选 Top10SellingProducts。 请注意两个属性（slicer 和 axis）均属于同一维度 [Product]。  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 产生以下结果集：  
  
|||||  
|-|-|-|-|  
||**分销商销售额**|**Discount Amount**|**PCT 折扣**|  
|**山地-200**|**$14356699.36**|**$19012.71**|**0.13%**|  
|**山地-100**|**$8568958.27**|**$139393.27**|**1.63%**|  
|**HL 山地框**|**$3365069.27**|**$174.11**|**0.01%**|  
|**山地-300**|**$1907249.38**|**$876.95**|**0.05%**|  
|**Mountain-500**|**$1067327.31**|**$17266.09**|**1.62%**|  
|**山地-400-W**|**$592450.05**|**$303.49**|**0.05%**|  
|**山地框**|**$521864.42**|**$252.41**|**0.05%**|  
|**ML 山地帧-W**|**$482953.16**|**$206.95**|**0.04%**|  
|**ML 山地框架**|**$343785.29**|**$161.82**|**0.05%**|  
|**Women's Mountain Shorts**|**$260304.09**|**$6675.56**|**2.56%**|  
  
 在上面的结果集中，我们看到 Top10SellingProducts 列表中有七种新产品，并且 Mountain-200、Mountain-100 和 HL Mountain Frame 移到了列表顶部。 在前面的结果集中，这三个值是混杂的。  
  
 这称为深度 Autoexists，因为对 Top10SellingProducts 集进行计算以符合查询的切片条件。 深度 Autoexists 意味着将对所有表达式进行计算，以便在应用了切片器表达式、轴中的嵌套 select 表达式等后到达可能的最深空间。  
  
 不过，有人可能希望能够对与 Preferred10Products 等效的 Top10SellingProducts 进行分析，如下面的示例所示：  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 产生以下结果集：  
  
|||||  
|-|-|-|-|  
||**分销商销售额**|**Discount Amount**|**PCT 折扣**|  
|**山地-200**|**$14356699.36**|**$19012.71**|**0.13%**|  
|**山地-100**|**$8568958.27**|**$139393.27**|**1.63%**|  
|**HL 山地框**|**$3365069.27**|**$174.11**|**0.01%**|  
  
 在上面的示例中，与预期的一样，切片生成的结果仅包含 Preferred10Products 中属于 [Product].[Product Line] 中的 [Mountain] 组的那些产品，因为 Preferred10Products 是一个常量表达式。  
  
 此结果集还可以理解为浅表 Autoexists。 这是因为该表达式是在切片子句之前计算的。 在上面的示例中，出于演示目的以介绍这一概念，该表达式是一个常量表达式。  
  
 可以使用 `Autoexists` 连接字符串属性在会话级修改 Autoexists 的行为。 下面的示例先打开一个新会话，然后将 *Autoexists=3* 属性添加到连接字符串。 必须打开新连接才能执行该示例。 在与 Autoexist 设置建立连接后，设置将一直有效，直到该连接结束。  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 下面的结果集现在显示 Autoexists 的浅表行为。  
  
|||||  
|-|-|-|-|  
||**分销商销售额**|**Discount Amount**|**PCT 折扣**|  
|**山地-200**|**$14356699.36**|**$19012.71**|**0.13%**|  
|**山地-100**|**$8568958.27**|**$139393.27**|**1.63%**|  
|**HL 山地框**|**$3365069.27**|**$174.11**|**0.01%**|  
  
 使用连接字符串中的 AUTOEXISTS = [1 | 2 | 3] 参数可以修改 Autoexists 行为;[&#40;xmla&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)和参数用法， <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>请参阅支持的 xmla 属性。  
  
## <a name="see-also"></a>另请参阅  
 [MDX &#40;Analysis Services 中的关键概念&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [多维数据集空间](cube-space.md)   
 [元](tuples.md)   
 [使用成员、元组和集 &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [直观合计和非直观合计](visual-totals-and-non-visual-totals.md)   
 [Mdx 语言参考 &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [MDX&#41; 引用 &#40;多维表达式](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
