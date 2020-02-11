---
title: 错误处理（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 611e7636f9a5cd6393da4a8412b6c02bcc9ddaf8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074679"
---
# <a name="error-handling-mdx"></a>错误处理 (MDX)
  每个多维数据集都可以控制多维表达式 (MDX) 脚本中处理错误的方法。 通过 `ScriptErrorHandlingMode` 枚举器完成错误处理。 此枚举器的可能值包括：  
  
 `IgnoreNone`  
 导致服务器在 MDX 脚本中发现任何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]错误时引发错误。  
  
 `IgnoreAll`  
 导致服务器忽略 MDX 脚本中包含错误（包括语法错误、名称解析错误等）的所有命令。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
