---
title: "Cousin (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUSIN
dev_langs: kbMDX
helpviewer_keywords: Cousin function
ms.assetid: 9a416685-d35d-4d9c-a9f6-4574cbe59aea
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fee1f82f0ed706a2ce75eedcb0968f007a0037c3
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="cousin-mdx"></a>Cousin (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回与指定的子成员在父成员下方具有相同的相对位置的子成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Ancestor_Member_Expression*  
 返回祖先成员的有效多维表达式 (MDX) 成员表达式。  
  
## <a name="remarks"></a>注释  
 此函数按各级别内的成员的顺序和位置进行操作。 如果有两个层次结构，第一个层次结构有四个级别，第二个层次结构有五个级别，则第一个层次结构的第三个级别与第二个层次结构的第三个级别是同级。  
  
## <a name="examples"></a>示例  
 下面的示例根据 2002 会计年度第四季度在 2003 会计年度中年级别上的祖先检索它的同级。 检索到的同级是 2003 会计年度第四季度。  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例根据 2002 会计年度 7 月在 2004 会计年度第二季度中季度级别上的祖先检索它的同级。 检索到的同级是 2003 年 10 月。  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
