---
title: 祖先 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ef9cccb488cebb08c1b9721c40cb8037ea8687a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739616"
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
  
## <a name="remarks"></a>Remarks  
 **祖先**函数将返回所有祖先构成的从成员本身至成员的层次结构的顶部; 更具体地说，它执行后序遍历层次结构对于所指定的成员，且然后返回所有祖先成员与成员相关，包括它自身，在一组。 这是与此相反[上级](../mdx/ancestor-mdx.md)函数，返回特定的祖先成员或祖先，在特定级别。  
  
## <a name="examples"></a>示例  
 下面的示例返回的分销商订单计数`[Sales Territory].[Northwest]`成员并从该成员的所有祖先**Adventure Works**多维数据集。 **祖先**函数构造一个集包括`[Sales Territory].[Northwest]`成员和 ROWS 轴其祖先。  
  
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
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
