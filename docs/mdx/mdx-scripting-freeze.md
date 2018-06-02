---
title: 冻结语句 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b7eb3a3939ce8525dc57d27a24ac005ecb2cf2d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579899"
---
# <a name="mdx-scripting---freeze"></a>MDX 脚本编写的冻结
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  将所指定子多维数据集的单元值锁定为其当前值。 锁定单元值后，更改其他单元不会影响锁定的单元。  
  
## <a name="syntax"></a>语法  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>参数  
 *Subcube_Expression*  
 返回子多维数据集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **冻结**语句锁定中指定的子多维数据集的单元格的值，防止后续语句在 MDX 中的更改其值在后续计算中使用的脚本将传递。  
  
 在下面的示例中，A 和 B 表示 MDX 计算脚本中的子多维数据集：  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 此时，A 和 B 都等于 3。  
  
 我们现在插入**冻结**函数来锁定中一个子多维数据集的单元格：  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 现在 A 等于 2，B 等于 3。  
  
## <a name="see-also"></a>请参阅  
 [MDX 脚本编写语句&#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
