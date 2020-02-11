---
title: 祖先（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 16c6f812d1d7cae5a81a8e64fb425f4d33f4cb5c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017057"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  返回指定成员的祖先集（包含该成员本身）。  
  
## <a name="syntax"></a>语法  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **祖先**函数将成员本身的所有上级从成员本身返回到成员层次结构的顶部;更具体地讲，它对指定成员的层次结构执行后序遍历，然后返回与该成员相关的所有祖先成员（包括其本身）。 这与[上级](../mdx/ancestor-mdx.md)函数不同，后者在特定级别返回特定的祖先成员或上级。  
  
## <a name="examples"></a>示例  
 下面的示例从`[Sales Territory].[Northwest]` **艾德工作**多维数据集中返回成员的分销商订单计数以及该成员的所有祖先。 该**祖先**函数为行轴构造包含`[Sales Territory].[Northwest]`成员及其祖先的集。  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
