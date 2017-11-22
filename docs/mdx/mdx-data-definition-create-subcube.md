---
title: "创建子多维数据集语句 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SUBCUBE
- CREATE SUBCUBE
- CREATE
- SUBCUBE
dev_langs: kbMDX
helpviewer_keywords:
- subcubes [MDX]
- CREATE SUBCUBE statement
ms.assetid: 15b6ac4c-b68a-4f9f-b33c-f5f7c4a74535
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5fd57d53dd07238781c452730f00e526fb6c2fff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---create-subcube"></a>MDX 数据定义-创建子多维数据集
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将所指定多维数据集或子多维数据集的多维数据集空间重定义给一个指定的子多维数据集。 此语句更改了用于后续操作的表观多维数据集空间。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE SUBCUBE Cube_Name AS Select_Statement  
                                                  | NON VISUAL ( Select_Statement )  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 为受限的多维数据集或透视提供名称的有效字符串表达式，该名称将作为子多维数据集的名称。  
  
 *Select_Statement*  
 不包含 WITH、NON EMPTY 或 HAVING 子句并且不要求维度或者单元属性的有效多维表达式 (MDX) SELECT 表达式。  
  
 请参阅[选择语句 &#40;MDX &#41;](../mdx/mdx-data-manipulation-select.md)有关在 Select 语句的详细的语法说明和**非直观**子句。  
  
## <a name="remarks"></a>注释  
 如果将默认成员排除在子多维数据集的定义之外，坐标将会相应更改。 对于可以聚合的属性，默认成员会被移到 [All] 成员中。 对于不可聚合的属性，默认成员会被移到该子多维数据集中存在的某一成员中。 下表包含子多维数据集和默认成员组合的示例。  
  
|原始默认成员|可以聚合|嵌套 select 语句|修改后的默认成员|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|Time.Year.All|是|{Time.Year.2003}|没有变化|  
|Time.Year。[1997]|是|{Time.Year.2003}|Time.Year.All|  
|Time.Year。[1997]|是|{Time.Year.2003}|Time.Year。[2003]|  
|Time.Year。[1997]|是|{Time.Year.2003, Time.Year.2004}|Time.Year.All|  
|Time.Year。[1997]|是|{Time.Year.2003, Time.Year.2004}|Time.Year.[2003] 或<br /><br /> Time.Year.[2004]|  
  
 子多维数据集中始终存在 [All] 成员。  
  
 删除子多维数据集时，也会删除在该子多维数据集的上下文中创建的会话对象。  
  
 有关子多维数据集的详细信息，请参阅[MDX &#40; 中生成子多维数据集MDX &#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md).  
  
## <a name="example"></a>示例  
 下例创建了一个子多维数据集，将表观多维数据集空间限制为与加拿大关联的成员。 然后，它使用**成员**函数以返回在国家/地区的所有成员级别 Geography 用户定义层次结构-返回仅的国家/地区加拿大。  
  
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
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$2,031,079.39|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$767,388.52|$175,002.81|$592,385.71|  
|Warehouse|$1,263,690.86|$331,169.64|$932,521.23|  
  
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
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$80,450,596.98|$571,297.93|$1,777,840.84|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 [All Products] 和 [All Resellers] 分别为列和行，包含所有成员（而不仅是可见成员）的总数。  
  
## <a name="see-also"></a>另请参阅  
 [MDX &#40; 中的重要概念Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX 脚本语句 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [DROP SUBCUBE 语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT 语句 &#40;MDX &#41;](../mdx/mdx-data-manipulation-select.md)  
  
  
