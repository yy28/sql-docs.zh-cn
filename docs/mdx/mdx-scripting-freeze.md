---
title: "冻结语句 (MDX) |Microsoft 文档"
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
f1_keywords: FREEZE
dev_langs: kbMDX
helpviewer_keywords:
- FREEZE statement
- locking cell values [MDX]
ms.assetid: 59f1e860-6f37-41af-97d6-7708bdaac933
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b447ef6b4c4699e652b6093c5d0a10e44ecb4d41
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
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
  
## <a name="remarks"></a>注释  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 脚本语句 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
