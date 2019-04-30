---
title: 冻结语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cd652a9f308bd7a564a61d165f9c47875a900737
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187567"
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
 **冻结**语句锁定指定的子多维数据集中的单元格的值，防止 MDX 中的后续语句更改其值在后续计算中使用的脚本将传递。  
  
 在下面的示例中，A 和 B 表示 MDX 计算脚本中的子多维数据集：  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 此时，A 和 B 都等于 3。  
  
 现在，我们将**冻结**函数来锁定 A 子多维数据集中的单元格：  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 现在 A 等于 2，B 等于 3。  
  
## <a name="see-also"></a>请参阅  
 [MDX 脚本编写语句 (MDX)](../mdx/mdx-scripting-statements-mdx.md)  
  
  
