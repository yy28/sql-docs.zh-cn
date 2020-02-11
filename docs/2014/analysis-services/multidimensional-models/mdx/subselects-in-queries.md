---
title: 查询中的嵌套 select 语句 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9e361798-688e-4b11-9eef-31fc793e8ba4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c9fb5d1300b6f50f7ef0a765881896069becf0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073901"
---
# <a name="subselects-in-queries"></a>查询中的嵌套 select 语句
  嵌套 select 语句表达式是嵌套的 SELECT 表达式，用于限制从其计算更外部的外部 SELECT 的多维数据集的空间。 嵌套 select 语句可用于定义要对其执行所有计算的新空间。  
  
## <a name="subselects-by-example"></a>嵌套 select 语句示例  
 让我们从一个示例开始，了解嵌套 select 语句如何帮助生成我们想要显示的结果。 假定要求您生成一个表，该表显示前 10 种产品在几年中的销售行为。  
  
 结果应该如下表所示：  
  
|||||  
|-|-|-|-|  
||Sum of Years|Year 1|...|  
|Sum of Top 10 Products||||  
|Product A||||  
|...||||  
  
 可以编写以下 MDX 表达式以获得类似上面的结果：  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].MEMBERS  
               , 10  
               , [Measures].[Sales Amount]  
               ) ON 1  
  FROM [Adventure Works]  
```  
  
 该查询返回以下结果：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$80,450,596.98|$8,065,435.31|$24,144,429.65|$32,202,669.43|$16,038,062.60|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
  
 上面的结果与我们所期望的结果非常接近；只是该查询返回 9 种而不是 10 种产品，并且 All Products 合计返回的是所有产品的总额，而没有返回前 9 种产品（在这个例子中）的总额。 下面的 MDX 查询将尝试解决上面的结果中遗留的问题：  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].CHILDREN, 10, [Measures].[Sales Amount]) ON 1  
  FROM [Adventure Works]  
```  
  
 该查询返回以下结果：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
|Road-150 Red, 62|$566,797.97|$234,018.86|$332,779.11|(null)|(null)|  
  
 上面的结果非常接近于期望的结果，只是缺少产品的总额。 此时，您可以开始微调上面的 MDX 表达式以便添加缺失的行；但是，这个任务执行起来显得相当麻烦。  
  
 解决该问题的另一个方法是开始考虑重新定义对其解析 MDX 表达式的多维数据集空间。 如果这个“新的”多维数据集只包含来自前 10 种产品的数据该怎么办？ 这样，该多维数据集将所有成员调整为仅是前 10 种产品，并且一个简单的查询现在就可以满足我们的需要。  
  
 下面的 MDX 表达式使用一个嵌套 select 语句，将多维数据集空间重新定义为前 10 种产品并且生成期望的结果：  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 上面的表达式返回以下结果：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$19,997,183.30|$1,696,815.63|$2,816,611.28|$7,930,797.72|$7,552,958.66|  
|Mountain-200 Silver, 38|$2,160,981.60|(null)|(null)|$1,024,359.10|$1,136,622.49|  
|Mountain-200 Silver, 42|$1,914,547.85|(null)|(null)|$903,061.68|$1,011,486.18|  
|Mountain-200 Silver, 46|$1,906,248.55|(null)|(null)|$877,077.79|$1,029,170.76|  
|Mountain-200 Black, 38|$1,811,229.02|(null)|$896,511.60|$914,717.43|(null)|  
|Mountain-200 Black, 38|$2,589,363.78|(null)|(null)|$1,261,406.37|$1,327,957.41|  
|Mountain-200 Black, 42|$2,265,485.38|(null)|(null)|$1,126,055.89|$1,139,429.49|  
|Mountain-200 Black, 46|$1,957,528.24|(null)|(null)|$946,453.88|$1,011,074.37|  
|Road-150 Red, 62|$1,769,096.69|$828,011.68|$941,085.01|(null)|(null)|  
|Road-150 Red, 56|$1,847,818.63|$868,803.96|$979,014.67|(null)|(null)|  
|Road-350-W Yellow, 48|$1,774,883.56|(null)|(null)|$877,665.59|$897,217.96|  
  
 上面的结果正是我们所期望的结果。  
  
 让我们回顾一下嵌套 select 语句为我们确切做了哪些工作。 该嵌套 select 语句返回了一个新的多维数据集，该多维数据集包含属于产品的所有其他维度；但在产品维度中，它将筛选与我们感兴趣的前 10 种产品匹配的所有成员。 这就像我们删除了未满足前 10 条件的所有数据并且重新生成了多维数据集。 在此示例中要理解的另一个重要概念就是对该多维数据集中所有其他维度的所有成员计算了前 10 种产品；这是因为在嵌套 select 语句中没有施加任何其他筛选限制。  
  
 嵌套 select 语句可以根据需要十分复杂；下面的示例将说明如何生成一个与上述表类似的表，但筛选 Sales Territory 维度上的 France 以及 Sales Channel 维度上的 Internet。  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
             , [Sales Territory].[Sales Territory].[Region].[France] on 1  
             ,  [Sales Channel].[Sales Channel].[Internet] on 2  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 生成以下结果：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$748,682.49|$32,204.43|$73,125.18|$269,506.56|$373,846.32|  
|Mountain-200 Silver, 38|$90,479.61|(null)|(null)|$41,759.82|$48,719.79|  
|Mountain-200 Silver, 42|$97,439.58|(null)|(null)|$39,439.83|$57,999.75|  
|Mountain-200 Silver, 46|$102,079.56|(null)|(null)|$27,839.88|$74,239.68|  
|Mountain-200 Black, 38|$26,638.28|(null)|$12,294.59|$14,343.69|(null)|  
|Mountain-200 Black, 38|$96,389.58|(null)|(null)|$41,309.82|$55,079.76|  
|Mountain-200 Black, 42|$80,324.65|(null)|(null)|$43,604.81|$36,719.84|  
|Mountain-200 Black, 46|$107,864.53|(null)|(null)|$45,899.80|$61,964.73|  
|Road-150 Red, 62|$46,517.51|$14,313.08|$32,204.43|(null)|(null)|  
|Road-150 Red, 56|$46,517.51|$17,891.35|$28,626.16|(null)|(null)|  
|Road-350-W Yellow, 48|$54,431.68|(null)|(null)|$15,308.91|$39,122.77|  
  
 上面的结果是在 France 通过 Internet 渠道销售的前 10 种产品。  
  
## <a name="subselect-statement"></a>嵌套 select 语句  
 该嵌套 select 语句的 BNF 是：  
  
```  
[WITH [<calc-clause> ...]]  
SELECT [<axis-spec> [, <axis-spec> ...]]  
FROM [<identifier> | (< sub-select-statement >)]  
[WHERE <slicer>]  
[[CELL] PROPERTIES <cellprop> [, <cellprop> ...]]  
  
< sub-select-statement > :=  
   SELECT [<axis-spec> [, <axis-spec> ...]]  
   FROM [<identifier> | (< sub-select-statement >)]  
   [WHERE <slicer>]  
  
```  
  
 该嵌套 select 语句是另一个 Select 语句，其中，轴规范和切片器规范筛选对其计算外部选择的多维数据集的空间。  
  
 在轴或切片器子句之一中指定了某一成员后，该成员及其祖先和后代将包括在该嵌套 select 语句的子多维数据集空间中；轴或切片器子句中所有未提及的同级成员及其后代将从子空间中筛选出来。 这样，外部选择的空间已限制为轴子句或切片器子句中的现有成员，且具有上述祖先和后代。  
  
 因为轴或切片器子句中所有未提及的维度的所有成员都属于该 select 语句的空间；所以，这些维度上所有成员的所有后代也是嵌套 select 语句空间的一部分。  
  
 子多维数据集空间中所有维度的所有成员将重新计算，以便反映新空间约束的影响。  
  
 下面的示例将说明上述内容；第一个 MDX 表达式将显示多维数据集中未筛选的值；第二个 MDX 将说明在嵌套 select 语句子句中进行筛选的影响：  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM [Adventure Works]  
```  
  
 返回以下值：  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$29,358,677.22|$80,450,596.98|  
|美国|$9,389,789.51|$80,450,596.98|  
|Oregon|$1,170,991.54|$80,450,596.98|  
|Portland|$110,649.54|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|西雅图|$75,164.86|$80,450,596.98|  
  
 在上面的示例中，Seattle 是 Washington 的子级，Portland 是 Oregon 的子级，Oregon 和 Washington 是 United States 的子级，United States 是 [Customer Geography].[All Customers] 的子级。 此示例中所有显示的成员都具有涉及父聚合值的其他同级；例如，Spokane、Tacoma 和 Everett 是 Seattle 的同级城市，并且它们都涉及 Washington Internet Sales Amount。 Reseller Sales Amount 值独立于 Customer Geography 属性；因此，所有值将显示在结果中。 下一个 MDX 表达式将说明嵌套 select 语句子句的筛选影响：  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
```  
  
 返回以下值：  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$2,467,248.34|$80,450,596.98|  
|美国|$2,467,248.34|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|西雅图|$75,164.86|$80,450,596.98|  
  
 上面的结果显示，只有 Washington State 的祖先和后代是计算外部选择语句的子空间的一部分；Oregon 和 Portland 已从子多维数据集中删除，因为在提及 Washington 时在嵌套 select 语句中未提及 Oregon 以及所有其他同级的州。  
  
 已对所有成员进行调整以便反映对 Washington 的筛选；不仅在 [Customer Geography] 维度中进行了调整，而且在与 [Customer Geography] 相交的所有其他维度中也进行调整。 不与 [Customer Geography] 相交的所有维度将在子多维数据集中保持不更改。  
  
 下面的两个 MDX 语句说明如何调整其他维度中的所有成员以便满足嵌套 select 语句的筛选效果。 第一个查询显示未更改的结果，第二个查询显示筛选的影响：  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM [Adventure Works]  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|组件|Mountain|道路|Touring|  
|All Customers|$29,358,677.22|$604,053.30|(null)|$10,251,183.52|$14,624,108.58|$3,879,331.82|  
|美国|$9,389,789.51|$217,168.79|(null)|$3,547,956.78|$4,322,438.41|$1,302,225.54|  
|Oregon|$1,170,991.54|$30,513.17|(null)|$443,607.98|$565,372.10|$131,498.29|  
|Portland|$110,649.54|$2,834.17|(null)|$47,099.91|$53,917.17|$6,798.29|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|西雅图|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|组件|Mountain|道路|Touring|  
|All Customers|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|美国|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|西雅图|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
 上面的结果显示，All Products 值已调整为预期的仅是来自 Washington State 的值。  
  
 对于嵌套 select 语句可以嵌套的深度没有限制，除非可用内存不支持。 最内部的嵌套 select 语句定义应用筛选的起始子空间并且向上传递到下一外部选择语句。 要注意的一个重要事项是，嵌套并非可交换操作；因此，所设置的嵌套的顺序可能会产生不同的结果。 下面的示例显示选择某一嵌套顺序时的差异。  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 返回以下结果。  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|澳大利亚|加拿大|Central|Northwest|Southwest|  
|All Products|$7,591,495.49|$1,281,059.99|$1,547,298.12|$600,205.79|$1,924,763.50|$2,238,168.08|  
|Mountain-200 Silver, 38|$1,449,576.15|$248,702.93|$275,052.45|$141,103.65|$349,487.01|$435,230.12|  
|Mountain-200 Black, 38|$1,722,896.50|$218,024.05|$418,726.43|$123,929.46|$486,694.63|$475,521.93|  
|Mountain-200 Black, 42|$1,573,655.14|$239,137.96|$319,921.61|$130,102.75|$420,445.84|$464,046.98|  
|Mountain-200 Black, 46|$1,420,500.58|$192,320.16|$230,875.99|$117,044.49|$424,813.66|$455,446.27|  
|Road-150 Red, 56|$1,424,867.11|$382,874.89|$302,721.64|$88,025.44|$243,322.36|$407,922.78|  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 返回以下结果。  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|澳大利亚|加拿大|Northwest|Southwest|英国|  
|All Products|$7,938,218.56|$1,096,312.24|$1,474,255.49|$2,042,674.72|$2,238,099.55|$1,086,876.56|  
|Mountain-200 Silver, 38|$1,520,958.53|$248,702.93|$275,052.45|$349,487.01|$435,230.12|$212,486.03|  
|Mountain-200 Silver, 42|$1,392,237.14|$198,127.15|$229,679.01|$361,233.58|$407,854.24|$195,343.16|  
|Mountain-200 Black, 38|$1,861,703.23|$218,024.05|$418,726.43|$486,694.63|$475,521.93|$262,736.19|  
|Mountain-200 Black, 42|$1,702,427.25|$239,137.96|$319,921.61|$420,445.84|$464,046.98|$258,874.87|  
|Mountain-200 Black, 46|$1,460,892.41|$192,320.16|$230,875.99|$424,813.66|$455,446.27|$157,436.31|  
  
 正如您所看到的，在这两个结果集之间存在差异。 第一个查询指明在前 5 个销售区域中哪些产品的销量最高；第二个查询指明对于前 5 种销售产品哪些区域的销量最高。  
  
### <a name="remarks"></a>备注  
 嵌套 select 语句具有以下限制：  
  
-   WHERE 子句不筛选子空间。  
  
-   WHERE 子句仅更改子多维数据集中的默认成员。  
  
-   轴子句中不允许 NON EMPTY 子句；请改用 [NonEmpty (MDX)](/sql/mdx/nonempty-mdx) 函数表达式。  
  
-   轴子句中不允许 HAVING 子句；请改用 [Filter (MDX)](/sql/mdx/filter-mdx) 函数表达式。  
  
-   默认情况下，嵌套 select 语句中不允许使用计算成员;但是，可以按会话更改此限制，方法是在[支持的 Xmla 属性 &#40;xmla&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)中`SubQueries` ，通过将值<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>分配`DBPROP_MSMD_SUBQUERIES`给或属性中的连接字符串属性。 有关计算成员行为的详细说明，请参阅[嵌套 select 语句和子多维数据中的计算成员](calculated-members-in-subselects-and-subcubes.md)，具体取决于`SubQueries`或`DBPROP_MSMD_SUBQUERIES`的值。  
  
  
