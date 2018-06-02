---
title: 计算 (MDX) 语句 |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 603d36e9c099ab6148e2e7c485f9c40ad99f63a8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579939"
---
# <a name="mdx-scripting---calculate"></a>MDX 脚本编写-计算
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用聚合值填充多维数据集中的每个单元。  
  
## <a name="syntax"></a>语法  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>参数  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>Remarks  
 使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建多维数据集时，CALCULATE 语句会自动作为第一个语句包含在 多维数据集的 MDX 脚本中。 CALCULATE 语句通知多维数据集中的每个单元从粒度较小的单元开始聚合。 聚合单元后，如果随后使用表达式填充粒度较小的单元，则会影响粒度较大的单元的聚合值。 您几乎总是希望这种聚合发生，但您可以删除它或使其他语句在此语句之前执行。  
  
 CALCULATE 语句无法包含在 MDX 脚本的嵌套子多维数据集中。 嵌套的子多维数据集是使用 SCOPE 语句定义的。 有关 SCOPE 语句的详细信息，请参阅[SCOPE 语句&#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
> [!NOTE]  
>  不对计算成员进行聚合。  
  
## <a name="see-also"></a>请参阅  
 [MDX 脚本编写语句&#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [MDX 脚本编写基础知识&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [定义赋值和其他脚本命令](../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)  
  
  
