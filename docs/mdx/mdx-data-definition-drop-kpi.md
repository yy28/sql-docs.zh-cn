---
title: 删除 KPI 语句 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- KPI
- DROP
- DROP KPI
- DROP_KPI
helpviewer_keywords:
- DROP KPI statement
- key performance indicators [MDX]
ms.assetid: d19c6809-b8a6-459d-8554-b41854f7cc45
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: e6e885e486033b0234841523b8193f37fe2e7563
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-kpi"></a>MDX 数据定义-删除 KPI
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  从指定多维数据集删除指定的关键绩效指标 (KPI)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP KPI CURRENTCUBE | Cube_Name.KPI_Name   
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 指定多维数据集名称的有效字符串。  
  
 *KPI_Name*  
 指定要删除的 KPI 的名称的有效字符串。  
  
## <a name="see-also"></a>另请参阅  
 [创建 KPI 语句&#40;MDX&#41;](../mdx/mdx-data-definition-create-kpi.md)   
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
