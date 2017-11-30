---
title: "计算 (MDX) 语句 |Microsoft 文档"
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
f1_keywords: CALCULATE
dev_langs: kbMDX
helpviewer_keywords: CALCULATE statement
ms.assetid: 41e196a1-d49e-487b-a42a-73e5d441ed1b
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fe79fa5b94e07be72408fc72b0df6e57fa467ee2
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-scripting---calculate"></a>MDX 脚本编写-计算
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用聚合值填充多维数据集中的每个单元。  
  
## <a name="syntax"></a>语法  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>参数  
 无  
  
## <a name="remarks"></a>注释  
 使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建多维数据集时，CALCULATE 语句会自动作为第一个语句包含在 多维数据集的 MDX 脚本中。 CALCULATE 语句通知多维数据集中的每个单元从粒度较小的单元开始聚合。 聚合单元后，如果随后使用表达式填充粒度较小的单元，则会影响粒度较大的单元的聚合值。 您几乎总是希望这种聚合发生，但您可以删除它或使其他语句在此语句之前执行。  
  
 CALCULATE 语句无法包含在 MDX 脚本的嵌套子多维数据集中。 嵌套的子多维数据集是使用 SCOPE 语句定义的。 有关 SCOPE 语句的详细信息，请参阅[SCOPE 语句 &#40;MDX &#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  不对计算成员进行聚合。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 脚本语句 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [MDX 脚本编写基础知识 &#40;Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [定义赋值和其他脚本命令](../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)  
  
  
