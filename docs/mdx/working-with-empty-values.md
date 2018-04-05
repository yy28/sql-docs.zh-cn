---
title: 使用空值 |Microsoft 文档
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
dev_langs:
- kbMDX
helpviewer_keywords:
- expressions [MDX], empty values
- empty values [MDX]
ms.assetid: 6338fb85-f513-4c3e-a774-4fd7c6986a91
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 37b91bc83640a10c9905726fdabb49c7816d77a1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="working-with-empty-values"></a>使用空值
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  空值表明特定成员、元组或单元是空的。 空单元值指明在基础事实表中找不到指定单元的数据，或者指定单元的元组代表不适用于多维数据集的成员组合。  
  
> [!NOTE]  
>  虽然空值有别于零值，但是通常大多数情况下都将空值作为零处理。  
  
 以下查询演示空值和零值的行为：  
  
```  
WITH  
//A calculated Product Category that always returns 0  
MEMBER [Product].[Category].[All Products].ReturnZero AS 0  
//Will return true for any null value  
MEMBER MEASURES.ISEMPTYDemo AS ISEMPTY([Measures].[Internet Tax Amount])  
//Will true for any null or zero value  
//To be clear: the expression 0=null always returns true in MDX  
MEMBER MEASURES.IsZero AS [Measures].[Internet Tax Amount]=0  
SELECT  
{[Measures].[Internet Tax Amount],MEASURES.ISEMPTYDemo,MEASURES.IsZero}  
ON COLUMNS,  
[Product].[Category].[Category].ALLMEMBERS  
ON ROWS  
FROM [Adventure Works]  
WHERE([Date].[Calendar].[Calendar Year].&[2001])  
```  
  
 以下信息适用于空值：  
  
-   [IsEmpty](../mdx/isempty-mdx.md)函数返回**TRUE**当且仅当标识由元组函数中指定的单元格为空。 否则，该函数返回**FALSE**。  
  
    > [!NOTE]  
    >  **IsEmpty**函数无法确定是否使用成员表达式，则返回空值。 若要确定是否从表达式返回了 null 成员，请使用[IS](../mdx/is-mdx.md)运算符。  
  
-   当空单元值是数字运算符（+、-、*、/）中任一运算符的一个操作数时，如果另一个操作数是非空值，空单元值将被作为零处理。 如果两个操作数都为空，数字运算符将返回空单元值。  
  
-   当空单元值是字符串串联运算符 (+) 的一个操作数时，如果另一个操作数是非空值，空单元值将被作为空字符串处理。 如果两个操作数都为空，字符串串联运算符将返回空单元值。  
  
-   当空单元值是比较运算符（=. <>，> =、 \<=、 >，<)、 空单元值将被视为零或空字符串，具体取决于数据的另一个操作数的类型是否是数字或字符串，分别。 如果两个操作数都为空，则两个操作数均作为零处理。  
  
-   当对数字值进行排序时，空单元值排在与零相同的位置。 在空单元值和零之间，空单元值排在零之前。  
  
-   当对字符串值进行排序时，空单元值排在与空字符串相同的位置。 在空单元值和空字符串之间，空单元值排在空字符串之前。  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>处理 MDX 语句和多维数据集中的空值  
 在多维表达式 (MDX) 语句中，可以查找空值，然后对包含有效（即不为空）数据的单元进行某些运算。 进行运算时消除空值很重要，因为如果包含空单元值，某些运算（如平均值）可能不准确。  
  
 如果空值存储在基础事实表数据中，则在处理多维数据集时，默认情况下这些空值将转换为零。 你可以使用**Null 处理**对度量值到控件的选项是否为 null 的事实数据转换为 0，转换为空值或甚至将引发错误处理过程。 如果您不希望空单元值出现在查询结果中，则应该创建消除空值或将空值替换为某些其他值的查询、计算成员或 MDX 脚本语句。  
  
 若要删除查询中的空行或空列，可以在轴设置定义之前使用 NON EMPTY 语句。 例如，以下查询仅返回 Product Category Bikes，因为它是 Calendar Year 2001 内销售的唯一 Category：  
  
 `SELECT`  
  
 `{[Measures].[Internet Tax Amount]}`  
  
 `ON COLUMNS,`  
  
 `//Comment out the following line to display all the empty rows for other Categories`  
  
 `NON EMPTY`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
 通常，若要从集中删除空元组，可以使用 NonEmpty 函数。 以下查询说明两个计算度量值，一个计算 Product Categories 的数目，另一个显示具有 [Internet Tax Amount] 和 Calendar Year 2001 度量值的 Product Categories 的数目：  
  
 `WITH`  
  
 `MEMBER MEASURES.CategoryCount AS`  
  
 `COUNT([Product].[Category].[Category].MEMBERS)`  
  
 `MEMBER MEASURES.NonEmptyCategoryCountFor2001 AS`  
  
 `COUNT(`  
  
 `NONEMPTY(`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `,([Date].[Calendar].[Calendar Year].&[2001], [Measures].[Internet Tax Amount])`  
  
 `))`  
  
 `SELECT`  
  
 `{MEASURES.CategoryCount,MEASURES.NonEmptyCategoryCountFor2001 }`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 有关详细信息，请参阅[NonEmpty &#40;MDX &#41;](../mdx/nonempty-mdx.md).  
  
## <a name="empty-values-and-comparison-operators"></a>空值和比较运算符  
 如果数据中存在空值，逻辑运算符和比较运算符有可能返回 TRUE 或 FALSE 以外的第三种结果 EMPTY。 这种对三值逻辑的需要是导致许多应用程序出错的根源。 下面这些表概括了引入空值比较的影响。  
  
 下表显示了对两个布尔操作数应用 AND 运算符的结果。  
  
|和|TRUE|EMPTY|FALSE|  
|---------|----------|-----------|-----------|  
|**TRUE**|TRUE|FALSE|FALSE|  
|**为空**|FALSE|EMPTY|FALSE|  
|**FALSE**|FALSE|FALSE|FALSE|  
  
 下表显示了对两个布尔操作数应用 OR 运算符的结果。  
  
|或|TRUE|FALSE|  
|--------|----------|-----------|  
|**TRUE**|TRUE|TRUE|  
|**为空**|TRUE|TRUE|  
|**FALSE**|TRUE|FALSE|  
  
 下表显示了 NOT 运算符如何求反或反转布尔运算符的结果。  
  
|要应用 NOT 运算符的布尔表达式|计算结果|  
|-------------------------------------------------------------|------------------|  
|TRUE|FALSE|  
|EMPTY|EMPTY|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 运算符参考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [表达式 &#40;MDX &#41;](../mdx/expressions-mdx.md)  
  
  
