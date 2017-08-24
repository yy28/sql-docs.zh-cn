---
title: "MeasureGroupMeasures (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- MeasureGroupMeasures function
ms.assetid: 69d9b205-1ca7-4741-9ca9-c7926bc87ead
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 17f8ba22b30fbfe925ae219a9f13bbdc5a9f1be0
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一组属于指定度量值组的度量值。  
  
## <a name="syntax"></a>語法  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>参数  
 *MeasureGroupName*  
 有效字符串表达式，其中包含要从中检索度量值集的度量值组的名称。  
  
## <a name="remarks"></a>備註  
 指定的字符串必须与度量值组名称精确匹配。 对于带空格的度量值组，不要求一定使用方括号。  
  
## <a name="example"></a>示例  
 下例返回 Adventure Works 多维数据集“Internet Sales”度量值组中的所有度量值。  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

