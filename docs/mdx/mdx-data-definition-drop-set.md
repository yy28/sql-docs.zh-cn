---
description: MDX 数据定义 - DROP SET
title: DROP SET 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5c4ca356847d75150aa098b331bdf0f8c8368bb6
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195602"
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
 提供多维数据集名称的有效字符串表达式。  
  
 *Set_Name*  
 有效字符串表达式，提供将要删除的命名集的名称。  
  
## <a name="remarks"></a>备注  
 有关命名集的详细信息，请参阅[在 MDX 中生成命名集 (MDX)](/analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets)。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 数据定义语句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
