---
title: 数据挖掘扩展插件 (DMX) 语法约定 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf80ef73ae3f55f58978d95b0d12b8c69b81dfff
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38037325"
---
# <a name="data-mining-extensions-dmx-syntax-conventions"></a>数据挖掘扩展插件 (DMX) 语法约定
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  中的数据挖掘扩展插件 (DMX) 参考文档[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]使用以下约定说明 DMX 语言。  
  
|约定|用法|  
|----------------|-----------|  
|**粗体**|必须是按原样正确键入的 DMX 关键字和文本。|  
|*斜体*|DMX 语法中用户提供的参数。|  
||（垂直条）|用于分隔括号或大括号内的各语法项。 只能选择其中一项。|  
|`[ ]`（方括号）|包含可选语法项。 不要键入方括号。|  
|{}（大括号）|包含必选的语法项。 不要键入大括号。|  
|, ...|指示逗号前面的项可重复任意次。 各项用逗号分隔。|  
|\<label> ::=|语法块的名称。 该约定用于对过长语法段或语法单元进行分组和标记，这些语法段或语法单元可在一条语句中的多个位置使用。 可以使用语法块的各个位置括在尖括号内，如的标签指示\<标签 >。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;引用](../dmx/data-mining-extensions-dmx-reference.md)  
  
  

