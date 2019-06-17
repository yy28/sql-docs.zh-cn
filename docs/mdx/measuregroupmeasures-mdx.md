---
title: MeasureGroupMeasures (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55e00420ad3f941d50d9179dcd4a87d678cc28a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267938"
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
