---
title: 祖先 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ASCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ascendants function
ms.assetid: a2baf4a2-7d66-4766-b708-739a3c21b09e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: df35665a82149bd133e4116d97cb739d70865ac7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定成员的祖先集（包含该成员本身）。  
  
## <a name="syntax"></a>语法  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
