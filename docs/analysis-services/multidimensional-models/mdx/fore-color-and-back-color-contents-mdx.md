---
title: "FORE_COLOR 和 BACK_COLOR 内容 (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FORE_COLOR 内容"
  - "背景 [MDX]"
  - "单元 [MDX]"
  - "颜色 [MDX]"
  - "存储单元颜色信息"
  - "单元背景"
  - "BACK_COLOR 内容"
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# FORE_COLOR 和 BACK_COLOR 内容 (MDX)
  **FORE_COLOR** 和 **BACK_COLOR** 单元属性分别以 Microsoft Windows 操作系统红绿蓝 (RGB) 格式存储单元的文本颜色信息和背景颜色信息。  
  
 普通 RGB 颜色的有效范围为 0 到 16,777,215 (&H00FFFFFF)。 此范围内数字的高位字节始终等于 0；低位的 3 个字节，从最低位字节到最高位字节分别决定了红色、绿色和蓝色的数量。 红色、绿色和蓝色成分分别由一个 0 到 255 (&HFF) 之间的数字表示。  
  
## 另请参阅  
 [使用单元属性 (MDX)](../../../analysis-services/multidimensional-models/mdx/using-cell-properties-mdx.md)  
  
  