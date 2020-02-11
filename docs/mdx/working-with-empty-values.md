---
title: 使用空值 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae8d6262f6502add09376b76a767a3076c830cb8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125849"
---
# <a name="working-with-empty-values"></a>使用空值


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
  
-   当且仅当函数中指定的元组所标识的单元格为空时， [IsEmpty](../mdx/isempty-mdx.md)函数才返回**TRUE** 。 否则，该函数返回**FALSE**。  
  
    > [!NOTE]  
    >  **IsEmpty**函数无法确定成员表达式是否返回 null 值。 若要确定是否从表达式返回 null 成员，请使用[is](../mdx/is-mdx.md)运算符。  
  
-   当空单元值是数字运算符（+、-、*、/）中任一运算符的一个操作数时，如果另一个操作数是非空值，空单元值将被作为零处理。 如果两个操作数都为空，数字运算符将返回空单元值。  
  
-   当空单元值是字符串串联运算符 (+) 的一个操作数时，如果另一个操作数是非空值，空单元值将被作为空字符串处理。 如果两个操作数都为空，字符串串联运算符将返回空单元值。  
  
-   当空单元值是比较运算符（=. <>、>=、 \<=、>、<），空单元值被视为零或空字符串，具体取决于另一个操作数的数据类型是数字还是字符串。 如果两个操作数都为空，则两个操作数均作为零处理。  
  
-   当对数字值进行排序时，空单元值排在与零相同的位置。 在空单元值和零之间，空单元值排在零之前。  
  
-   当对字符串值进行排序时，空单元值排在与空字符串相同的位置。 在空单元值和空字符串之间，空单元值排在空字符串之前。  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>处理 MDX 语句和多维数据集中的空值  
 在多维表达式 (MDX) 语句中，可以查找空值，然后对包含有效（即不为空）数据的单元进行某些运算。 进行运算时消除空值很重要，因为如果包含空单元值，某些运算（如平均值）可能不准确。  
  
 如果空值存储在基础事实表数据中，则在处理多维数据集时，默认情况下这些空值将转换为零。 您可以对度量值使用**Null 处理**选项，以控制 null 事实是否转换为0，转换为空值，甚至在处理过程中引发错误。 如果您不希望空单元值出现在查询结果中，则应该创建消除空值或将空值替换为某些其他值的查询、计算成员或 MDX 脚本语句。  
  
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
  
 有关详细信息，请参阅非[空 &#40;MDX&#41;](../mdx/nonempty-mdx.md)。  
  
## <a name="empty-values-and-comparison-operators"></a>空值和比较运算符  
 如果数据中存在空值，逻辑运算符和比较运算符有可能返回 TRUE 或 FALSE 以外的第三种结果 EMPTY。 这种对三值逻辑的需要是导致许多应用程序出错的根源。 下面这些表概括了引入空值比较的影响。  
  
 下表显示了对两个布尔操作数应用 AND 运算符的结果。  
  
|和|TRUE|EMPTY|FALSE|  
|---------|----------|-----------|-----------|  
|**TRUE**|TRUE|FALSE|FALSE|  
|**EMPTY**|FALSE|EMPTY|FALSE|  
|**FALSE**|FALSE|FALSE|FALSE|  
  
 下表显示了对两个布尔操作数应用 OR 运算符的结果。  
  
|或|TRUE|FALSE|  
|--------|----------|-----------|  
|**TRUE**|TRUE|TRUE|  
|**EMPTY**|TRUE|TRUE|  
|**FALSE**|TRUE|FALSE|  
  
 下表显示了 NOT 运算符如何求反或反转布尔运算符的结果。  
  
|要应用 NOT 运算符的布尔表达式|计算结果|  
|-------------------------------------------------------------|------------------|  
|TRUE|FALSE|  
|EMPTY|EMPTY|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX&#41;&#40;表达式](../mdx/expressions-mdx.md)  
  
  
