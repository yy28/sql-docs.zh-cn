---
title: "KPIWeight (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: KPIWeight function
ms.assetid: 6d585c76-b4c4-437f-8433-cfa4e6057af1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 06f1c5e8a1ed26355f2fbe71f00e9f7b2125248b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="kpiweight-mdx"></a>KPIWeight (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定关键绩效指标 (KPI) 的权重。  
  
## <a name="syntax"></a>语法  
  
```  
  
KPIWeight(KPI_Name)  
```  
  
## <a name="arguments"></a>参数  
 *KPI_Name*  
 一个有效的字符串表达式，指定 KPI 的名称。  
  
## <a name="remarks"></a>注释  
 返回的值是 KPI 在父级中所占的比例。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
