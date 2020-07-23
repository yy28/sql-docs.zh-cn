---
title: 双斜杠（注释）（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e53b3823bd824ae1caab05ffe24cb8a3e904994d
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969783"
---
# <a name="double-slash-comment-dmx"></a>双斜杠（注释）（DMX）
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 您可以在数据挖掘扩展 (DMX) 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>参数  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>备注  
 只将 // 用于单行注释。 使用//插入的注释由换行符分隔。  
  
 注释没有最大长度限制。  
  
 有关如何在 DMX 中使用不同种类的注释的详细信息，请参阅[&#40;dmx&#41;的注释](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [斜杠星形 &#40;注释&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [--&#40;注释&#41; &#40;DMX&#41; 摘要](../dmx/comment-dmx-summary.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
