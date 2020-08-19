---
description: MDX 数据定义 - DROP CELL CALCULATION
title: 删除 MDX) 的单元格计算语句 (|Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a407d6325168e2287fc6b815b3b45f0130dd1a4d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429799"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>MDX 数据定义 - DROP CELL CALCULATION


  删除指定的单元计算。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供多维数据集表达式名称的有效字符串表达式。  
  
 *CellCalc_Name*  
 提供要删除的单元计算名称的有效字符串表达式。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;MDX 创建单元计算语句&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Mdx 数据定义语句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
