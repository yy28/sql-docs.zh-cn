---
title: MeasureGroupMeasures （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45d7adc5e1f4e103790d9d067bc4876fb5b134d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68033873"
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)


  返回一组属于指定度量值组的度量值。  
  
## <a name="syntax"></a>语法  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>参数  
 *MeasureGroupName*  
 有效字符串表达式，其中包含要从中检索度量值集的度量值组的名称。  
  
## <a name="remarks"></a>备注  
 指定的字符串必须与度量值组名称精确匹配。 对于带空格的度量值组，不要求一定使用方括号。  
  
## <a name="example"></a>示例  
 下例返回 Adventure Works 多维数据集“Internet Sales”度量值组中的所有度量值。  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
