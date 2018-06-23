---
title: 用户定义的成员属性 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ba34243609b796eef635fc3b55cd99ef4f225638
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018042"
---
# <a name="user-defined-member-properties-mdx"></a>用户定义的成员属性 (MDX)
  用户定义的成员属性可作为属性关系添加到维度的特定命名级别中。 无法将用户定义的成员属性添加到`(All)`级别的层次结构，或层次结构自身。  
  
## <a name="creating-user-defined-member-properties"></a>创建用户定义的成员属性  
 用户定义的成员属性可以通过用户界面或通过编程方式添加到基于服务器的维度或多维数据集中。  
  
-   若要通过用户界面添加用户定义的成员属性，请使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的维度设计器。 有关详细信息，请参阅 [定义属性关系](../attribute-relationships-define.md)。  
  
-   若要通过编程方式添加用户定义的成员属性，您的应用程序可以使用 Analysis Manager 对象 (AMO) 或者结合使用 XML for Analysis (XMLA) 和 Analysis Services 脚本语言 (ASSL)。 有关详细信息，请参阅 [属性关系](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
## <a name="retrieving-user-defined-member-properties"></a>检索用户定义的成员属性  
 您可以检索用户定义的成员属性使用`PROPERTIES`关键字或[属性](/sql/mdx/properties-mdx)函数。  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>使用 PROPERTIES 关键字检索用户定义的成员属性  
 检索用户定义的成员属性的语法与用来检索内部级别成员属性的语法相似，如下列语法所示：  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 `PROPERTIES`关键字出现在轴规范的集表达式之后。 例如，下面的 MDX 查询`PROPERTIES`关键字检索`List Price`和`Dealer Price`用户定义的成员属性和组表达式，标识产品销售的年 1 月后，将显示：  
  
```  
SELECT   
   CROSSJOIN([Ship Date].[Calendar].[Calendar Year].Members,   
             [Measures].[Sales Amount]) ON COLUMNS,  
   NON EMPTY Product.Product.MEMBERS  
   DIMENSION PROPERTIES   
              Product.Product.[List Price],  
              Product.Product.[Dealer Price]  ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Month of Year].[January])   
```  
  
### <a name="using-the-properties-function-to-retrieve-user-defined-member-properties"></a>使用 Properties 函数检索用户定义的成员属性  
 也可以使用 `Properties` 函数访问自定义成员属性。 例如，下面的 MDX 查询使用`WITH`关键字来创建计算的成员组成`List Price`成员属性：  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 有关生成计算成员的详细信息，请参阅[在 MDX 中生成计算成员 (MDX)](mdx-calculated-members-building-calculated-members.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用成员属性&#40;MDX&#41;](mdx-member-properties.md)   
 [属性&#40;MDX&#41;](/sql/mdx/properties-mdx)  
  
  
