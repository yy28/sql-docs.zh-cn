---
title: "用户定义的成员属性 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
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
helpviewer_keywords: custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: eaeb79931b4c9c57088ada093148047a26b614d2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-member-properties---user-defined-member-properties"></a>MDX 成员属性的用户定义的成员属性
  用户定义的成员属性可作为属性关系添加到维度的特定命名级别中。 用户定义的成员属性不能添加到层次结构的 **(All)** 级别，也不能添加到层次结构本身中。  
  
## <a name="creating-user-defined-member-properties"></a>创建用户定义的成员属性  
 用户定义的成员属性可以通过用户界面或通过编程方式添加到基于服务器的维度或多维数据集中。  
  
-   若要通过用户界面添加用户定义的成员属性，请使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的维度设计器。 有关详细信息，请参阅 [定义属性关系](../../../analysis-services/multidimensional-models/attribute-relationships-define.md)。  
  
-   若要通过编程方式添加用户定义的成员属性，您的应用程序可以使用 Analysis Manager 对象 (AMO) 或者结合使用 XML for Analysis (XMLA) 和 Analysis Services 脚本语言 (ASSL)。 有关详细信息，请参阅 [属性关系](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
## <a name="retrieving-user-defined-member-properties"></a>检索用户定义的成员属性  
 可以使用 **PROPERTIES** 关键字或 [Properties](../../../mdx/properties-mdx.md) 函数检索用户定义的成员属性。  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>使用 PROPERTIES 关键字检索用户定义的成员属性  
 检索用户定义的成员属性的语法与用来检索内部级别成员属性的语法相似，如下列语法所示：  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 **PROPERTIES** 关键字出现在轴规范的集表达式之后。 例如，以下 MDX 查询中的 **PROPERTIES** 关键字将检索用户定义成员属性 `List Price` 和 `Dealer Price` ，并显示在标识一月份售出产品的集表达式之后：  
  
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
 也可以使用 **Properties** 函数访问自定义成员属性。 例如，以下 MDX 查询使用 **WITH** 关键字创建包含 `List Price` 成员属性的计算成员：  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 有关生成计算成员的详细信息，请参阅[在 MDX 中生成计算成员 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用成员属性 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [属性 &#40;MDX &#41;](../../../mdx/properties-mdx.md)  
  
  
