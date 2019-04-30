---
title: CALL 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4052134e9fd7d3c6877894c61480897e40982b59
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187674"
---
# <a name="mdx-data-manipulation---call"></a>MDX 数据操作 - CALL


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
  
## <a name="remarks"></a>备注  
 **调用**语句运行指定已注册存储的过程，也可以选择包含一个或多个参数指定的存储过程。 **调用**语句是只适用于返回结合的存储过程。 此语句不能在 MDX 表达式中与其他函数或运算符结合使用。 返回值的注册存储过程可以在 MDX 表达式中直接调用，并可以与其他 MDX 函数和运算符结合使用。  
  
 如果未指定多维数据集，该语句将在当前多维数据集上运行存储过程。  
  
> [!NOTE]  
>  如果未在客户端上注册存储的过程**调用**语句尝试通过的实例调用存储的过程[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [MDX 数据操作语句&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [使用存储过程 &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
