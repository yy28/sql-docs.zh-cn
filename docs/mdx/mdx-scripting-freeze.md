---
description: FREEZE 语句 (MDX)
title: " (MDX) 冻结语句 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41c71987fec932b2693740792a8d86e200fcf526
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429739"
---
# <a name="mdx-scripting---freeze"></a>MDX 脚本 - FREEZE


  将所指定子多维数据集的单元值锁定为其当前值。 锁定单元值后，更改其他单元不会影响锁定的单元。  
  
## <a name="syntax"></a>语法  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>参数  
 *Subcube_Expression*  
 返回子多维数据集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **冻结**语句锁定指定子多维数据集中的单元的值，阻止 MDX 脚本中的后续语句在后续计算传递中更改其值。  
  
 在下面的示例中，A 和 B 表示 MDX 计算脚本中的子多维数据集：  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 此时，A 和 B 都等于 3。  
  
 现在，我们插入了 **冻结** 函数以锁定子多维数据集中的单元：  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 现在 A 等于 2，B 等于 3。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 脚本编写语句 (MDX)](../mdx/mdx-scripting-statements-mdx.md)  
  
  
