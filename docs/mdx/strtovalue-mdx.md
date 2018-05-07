---
title: StrToValue (MDX) |Microsoft 文档
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
- STRTOVALUE
dev_langs:
- kbMDX
helpviewer_keywords:
- StrToValue function
ms.assetid: 118a9c4f-74a3-48d5-a4f4-318664bc51bc
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c9df8d31e49019abf730f70664a74c50d7bdc678
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回多维表达式 (MDX) 格式的字符串指定的数值。  
  
## <a name="syntax"></a>语法  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>参数  
 *MDX_Expression*  
 直接或间接解析为单个单元的有效字符串表达式。  
  
## <a name="remarks"></a>注释  
 **StrToValue**函数返回由 MDX 表达式指定的数字值。 **StrToValue**函数通常用于与用户定义的函数返回一个 MDX 表达式从一个外部函数回可被解析为单个单元格的 MDX 语句。  
  
-   如果使用 CONSTRAINED 标志，则 MDX 表达式只能包含一个标量值。 通过指定字符串，使用 CONSTRAINED 标志可降低发生注入攻击的风险。 如果提供的 MDX 表达式不能直接解析为标量值，则会出现下列出错信息：“违反了 STRTOVALUE 函数中 CONSTRAINED 标志所规定的限制。”  
  
-   当未使用 CONSTRAINED 标志时，指定的 MDX 表达式的复杂程度不受限制，只要该表达式可解析为能够返回单个单元的有效多维表达式 (MDX) 即可。  
  
> [!NOTE]  
>  如果 MDX 表达式的结果以文本方式存储，并且您希望对返回值执行算术运算，那么将该结果作为数值返回将十分有用。  
  
## <a name="example"></a>示例  
 下面的示例使用**StrToValue**函数以返回一个值为每个自行车的权重。  
  
```  
WITH MEMBER Measures.x AS   
StrToValue   
   ([Product].[Product].CurrentMember.Properties ('Weight')  
   ,CONSTRAINED  
   )  
SELECT Measures.x ON 0  
,[Product].[Product].[Product].Members ON 1  
FROM [Adventure Works]  
WHERE [Product].[Product Categories].[Bikes]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
