---
title: "错误处理 (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "脚本 [MDX], 异常"
  - "异常 [MDX]"
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# 错误处理 (MDX)
  每个多维数据集都可以控制多维表达式 (MDX) 脚本中处理错误的方法。 通过 **ScriptErrorHandlingMode** 枚举器完成错误处理。 此枚举器的可能值包括：  
  
 **IgnoreNone**  
 当 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 在 MDX 脚本中发现任何错误时，会导致服务器引发错误。  
  
 **IgnoreAll**  
 导致服务器忽略 MDX 脚本中包含错误（包括语法错误、名称解析错误等）的所有命令。  
  
## 另请参阅  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  