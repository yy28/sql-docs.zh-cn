---
title: DROP SET 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 26c5ebe206ed9d8530a7158b464e974920dd878e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284968"
---
# <a name="mdx-data-definition---drop-set"></a>MDX 数据定义 - DROP SET


  删除一个命名集。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP [SESSION] SET   
   <Cube_Reference>.Set_Name   
               [,<Cube_Reference>.Set_Name ...n]  
  
<Cube_Reference> ::= {CURRENTCUBE | Cube_Name}  
  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供的多维数据集名称的有效字符串表达式。  
  
 *Set_Name*  
 有效字符串表达式，提供将要删除的命名集的名称。  
  
## <a name="remarks"></a>备注  
 有关命名集的详细信息，请参阅[在 MDX 中生成命名集 (MDX)](../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)。  
  
## <a name="see-also"></a>请参阅  
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
