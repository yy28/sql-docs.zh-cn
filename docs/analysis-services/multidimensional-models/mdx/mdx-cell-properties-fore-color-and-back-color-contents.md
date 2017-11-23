---
title: "FORE_COLOR 和 BACK_COLOR 内容 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 15eccb9f4951a52bc1cfcf62e15e85eb245eb5f9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-cell-properties---forecolor-and-backcolor-contents"></a>MDX 单元格属性-FORE_COLOR 和 BACK_COLOR 内容
  **FORE_COLOR** 和 **BACK_COLOR** 单元属性分别以 Microsoft Windows 操作系统红绿蓝 (RGB) 格式存储单元的文本颜色信息和背景颜色信息。  
  
 普通 RGB 颜色的有效范围为 0 到 16,777,215 (&H00FFFFFF)。 此范围内数字的高位字节始终等于 0；低位的 3 个字节，从最低位字节到最高位字节分别决定了红色、绿色和蓝色的数量。 红色、绿色和蓝色成分分别由一个 0 到 255 (&HFF) 之间的数字表示。  
  
## <a name="see-also"></a>另请参阅  
 [使用单元属性 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)  
  
  
