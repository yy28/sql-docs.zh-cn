---
title: FORE_COLOR 和 BACK_COLOR 内容 (MDX) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e79767762431ca6f95badfde8cee40ea65975a4a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-cell-properties---forecolor-and-backcolor-contents"></a>MDX 单元格属性-FORE_COLOR 和 BACK_COLOR 内容
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  **FORE_COLOR** 和 **BACK_COLOR** 单元属性分别以 Microsoft Windows 操作系统红绿蓝 (RGB) 格式存储单元的文本颜色信息和背景颜色信息。  
  
 普通 RGB 颜色的有效范围为 0 到 16,777,215 (&H00FFFFFF)。 此范围内数字的高位字节始终等于 0；低位的 3 个字节，从最低位字节到最高位字节分别决定了红色、绿色和蓝色的数量。 红色、绿色和蓝色成分分别由一个 0 到 255 (&HFF) 之间的数字表示。  
  
## <a name="see-also"></a>另请参阅  
 [使用单元属性 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)  
  
  
