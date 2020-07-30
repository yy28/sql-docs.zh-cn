---
title: CREATE 子多维数据集语句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1034d96ce0d683d38139636d53471d23581807a1
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362797"
---
# <a name="mdx-data-definition---create-subcube"></a>MDX 数据定义 - CREATE SUBCUBE


  将所指定多维数据集或子多维数据集的多维数据集空间重定义给一个指定的子多维数据集。 此语句更改了用于后续操作的表观多维数据集空间。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE SUBCUBE Cube_Name AS Select_Statement  
                                                  | NON VISUAL ( Select_Statement )  
```  
  
## <a name="arguments"></a>自变量  
 *Cube_Name*  
 为受限的多维数据集或透视提供名称的有效字符串表达式，该名称将作为子多维数据集的名称。  
  
 *Select_Statement*  
 不包含 WITH、NON EMPTY 或 HAVING 子句并且不要求维度或者单元属性的有效多维表达式 (MDX) SELECT 表达式。  
  
 有关 Select 语句和**非可视**子句的详细语法说明，请参阅[SELECT 语句 &#40;MDX&#41;](../mdx/mdx-data-manipulation-select.md) 。  
  
## <a name="remarks"></a>备注  
 如果将默认成员排除在子多维数据集的定义之外，坐标将会相应更改。 对于可以聚合的属性，默认成员会被移到 [All] 成员中。 对于不可聚合的属性，默认成员会被移到该子多维数据集中存在的某一成员中。 下表包含子多维数据集和默认成员组合的示例。  
  
|原始默认成员|可以聚合|嵌套 select|修改后的默认成员|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|Time.Year.All|是|{Time.Year.2003}|没有变化|  
|Year。[1997]|是|{Time.Year.2003}|Time.Year.All|  
|Year。[1997]|否|{Time.Year.2003}|Year。[2003]|  
|Year。[1997]|是|{Time.Year.2003, Time.Year.2004}|Time.Year.All|  
|Year。[1997]|否|{Time.Year.2003, Time.Year.2004}|Time.Year.[2003] 或<br /><br /> Time.Year.[2004]|  
  
 子多维数据集中始终存在 [All] 成员。  
  
 删除子多维数据集时，也会删除在该子多维数据集的上下文中创建的会话对象。  
  
 有关子多维数据的详细信息，请参阅[在 mdx 中生成子多维数据 &#40;mdx&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx)。  
  
## <a name="example"></a>示例  
 下例创建了一个子多维数据集，将表观多维数据集空间限制为与加拿大关联的成员。 然后，它使用**MEMBERS**函数返回 Geography 用户定义的层次结构的国家/地区级别的所有成员-仅返回加拿大国家/地区。  
  
```  
CREATE SUBCUBE [Adventure Works] AS  
   SELECT [Geography].[Country].&[Canada] ON 0  
   FROM [Adventure Works]  
  
SELECT [Geography].[Country].[Country].MEMBERS ON 0  
   FROM [Adventure Works]  
  
```  
  
 下例创建了一个子多维数据集，将表观多维数据集空间限制为 Products.Category 中的 {Accessories, Clothing} 成员和 Resellers.[Business Type] 中的 {[Value Added Reseller] , [Warehouse]} 成员。  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works]`  
  
 利用下面的 MDX 查询 Products.Category 和 Resellers.[Business Type] 中所有成员的子多维数据集：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 生成下列结果：  
  
|业务类型 + 类别|All Products|配件|Clothing|  
|-|-|-|-|  
|All Resellers|$2031079.39|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$767388.52|$175,002.81|$592,385.71|  
|Warehouse|$1263690.86|$331,169.64|$932,521.23|  
  
 使用 NON VISUAL 子句删除并重新创建子多维数据集将会创建一个子多维数据集，用于保留 Products.Category 和 Resellers.[Business Type] 中所有成员的实际总数，不论他们在子多维数据集中是否可见。  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 从上面发出同一 MDX 查询。  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 生成以下不同的结果：  
  
|业务类型 + 类别|All Products|配件|Clothing|  
|-|-|-|-|  
|All Resellers|$80,450,596.98|$571,297.93|$1,777,840.84|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 [All Products] 和 [All Resellers] 分别为列和行，包含所有成员（而不仅是可见成员）的总数。  
  
## <a name="see-also"></a>另请参阅  
 [MDX &#40;Analysis Services 中的关键概念&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)   
 [Mdx 脚本语句 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [&#40;MDX&#41;删除子多维数据集语句](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT 语句 (MDX)](../mdx/mdx-data-manipulation-select.md)  
  
  
