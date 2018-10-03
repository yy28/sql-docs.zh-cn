---
title: 错误处理 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57b7320e8d09a3106d29a7f4c53c14a52afaadd7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187977"
---
# <a name="error-handling-mdx"></a>错误处理 (MDX)
  每个多维数据集都可以控制多维表达式 (MDX) 脚本中处理错误的方法。 通过完成错误处理`ScriptErrorHandlingMode`枚举器。 此枚举器的可能值包括：  
  
 `IgnoreNone`  
 当 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 在 MDX 脚本中发现任何错误时，会导致服务器引发错误。  
  
 `IgnoreAll`  
 导致服务器忽略 MDX 脚本中包含错误（包括语法错误、名称解析错误等）的所有命令。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
