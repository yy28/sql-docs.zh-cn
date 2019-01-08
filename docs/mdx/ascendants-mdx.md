---
title: 祖先 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3122b3aa2f53da69f88e6ffad508f12c8e10da1c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52404342"
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
 **祖先**函数可返回所有成员的祖先成员的层次结构顶部该成员本身; 具体而言，它执行后序遍历层次结构的指定成员，然后返回与成员，包括其本身，在一组相关的所有祖先成员。 这是与此相反[祖先](../mdx/ancestor-mdx.md)函数，返回的特定祖先成员或祖先的特定级别。  
  
## <a name="examples"></a>示例  
 下面的示例返回的分销商订单计数`[Sales Territory].[Northwest]`成员并从该成员的所有祖先**Adventure Works**多维数据集。 **祖先**函数将构造的集包括`[Sales Territory].[Northwest]`成员和 ROWS 轴其祖先。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
