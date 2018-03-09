---
title: "级别 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Levels
dev_langs: kbMDX
helpviewer_keywords: Levels function
ms.assetid: 1a989cc9-8aa8-4ec3-b5e9-795d6fa84983
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1898b87749b8ae2921e71d391f8bbae3374d893b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="levels-mdx"></a>Levels (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回由数值表达式指定在维度或层次结构中的位置的级别，或返回由字符串表达式指定名称的级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *Level_Number*  
 指定级别号的有效数值表达式。  
  
 *Level_Name*  
 指定级别名称的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 如果指定级别号，则**级别**函数返回与指定的从零开始位置相关联的级别。  
  
 如果指定级别的名称，则**级别**函数将返回指定的级别。  
  
> [!NOTE]  
>  将字符串表达式语法用于用户定义的函数。  
  
## <a name="examples"></a>示例  
 以下示例说明了每个**级别**函数语法。  
  
### <a name="numeric"></a>数字  
 以下示例返回国家（地区）级别：  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 以下示例返回国家（地区）级别：  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
