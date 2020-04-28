---
title: 计算语句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a873c2a6a60e3e6283c3c24fa4b9d28757e57ffb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893355"
---
# <a name="mdx-scripting---calculate"></a>MDX 脚本 - CALCULATE


  使用聚合值填充多维数据集中的每个单元。  
  
## <a name="syntax"></a>语法  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>参数  
 无  
  
## <a name="remarks"></a>备注  
 使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建多维数据集时，CALCULATE 语句会自动作为第一个语句包含在 多维数据集的 MDX 脚本中。 CALCULATE 语句通知多维数据集中的每个单元从粒度较小的单元开始聚合。 聚合单元后，如果随后使用表达式填充粒度较小的单元，则会影响粒度较大的单元的聚合值。 您几乎总是希望这种聚合发生，但您可以删除它或使其他语句在此语句之前执行。  
  
 CALCULATE 语句无法包含在 MDX 脚本的嵌套子多维数据集中。 嵌套的子多维数据集是使用 SCOPE 语句定义的。 有关 SCOPE 语句的详细信息，请参阅[Scope 语句 &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
> [!NOTE]  
>  不对计算成员进行聚合。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 脚本语句 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [MDX 脚本编写基础 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [定义赋值和其他脚本命令](https://docs.microsoft.com/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
  
