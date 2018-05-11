---
title: 错误处理 (MDX) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7575a598342dfabd66bc15a8f67b3b8ca70f690
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="error-handling-mdx"></a>错误处理 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  每个多维数据集都可以控制多维表达式 (MDX) 脚本中处理错误的方法。 通过 **ScriptErrorHandlingMode** 枚举器完成错误处理。 此枚举器的可能值包括：  
  
 **IgnoreNone**  
 当 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 在 MDX 脚本中发现任何错误时，会导致服务器引发错误。  
  
 **IgnoreAll**  
 导致服务器忽略 MDX 脚本中包含错误（包括语法错误、名称解析错误等）的所有命令。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
