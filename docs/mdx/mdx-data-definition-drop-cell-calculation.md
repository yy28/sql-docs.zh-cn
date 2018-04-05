---
title: 删除单元格计算语句 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Calculation
- DROP
- DROP_CELL_CALCULATION
- CELL CALCULATION
- DROP CELL
- cell
- DROP CELL CALCULATION
dev_langs:
- kbMDX
helpviewer_keywords:
- deleting calculations
- dropping calculations
- removing calculations
- DROP CELL CALCULATION statement
- calculations [SQL Server]
- cubes [Analysis Services], calculations
ms.assetid: 77caedf4-dd96-4eac-a5e4-fd82148a44a7
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e84207fc0354c7599feb823f0b54b27fdc164619
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>MDX 数据定义-删除单元计算
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [创建单元格计算语句 &#40;MDX &#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [MDX 数据定义语句 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
