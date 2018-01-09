---
title: "CALL 语句 (MDX) |Microsoft 文档"
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
f1_keywords: CALL
dev_langs: kbMDX
helpviewer_keywords:
- voids [MDX]
- stored procedures [MDX]
- CALL statement
ms.assetid: b534a20b-924c-43b8-832d-24e57d50425c
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6b3e7d095a7957c8d5af8dc497bb7a9d884005b8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-manipulation---call"></a>MDX 数据操作的调用
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  运行一个存储过程，它在当前作用域或指定的多维数据集（可选）中返回空值。  
  
## <a name="syntax"></a>语法  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>参数  
 *SP_Name*  
 提供存储过程名称的有效字符串表达式。  
  
 *SP_Argument*  
 向被调用存储过程提供参数的有效字符串表达式。  
  
 *Cube_Expression*  
 提供多维数据集名称的有效字符串多维数据集表达式。  
  
## <a name="remarks"></a>Remarks  
 **调用**语句运行指定已注册存储的过程，有选择性地包括指定的存储过程的一个或多个自变量。 **调用**语句是返回空白的存储过程仅适用于。 此语句不能在 MDX 表达式中与其他函数或运算符结合使用。 返回值的注册存储过程可以在 MDX 表达式中直接调用，并可以与其他 MDX 函数和运算符结合使用。  
  
 如果未指定多维数据集，该语句将在当前多维数据集上运行存储过程。  
  
> [!NOTE]  
>  如果未在客户端上注册存储的过程**调用**语句尝试从的实例调用存储的过程[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 数据操作语句 &#40;MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [使用存储的过程 &#40;MDX &#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
