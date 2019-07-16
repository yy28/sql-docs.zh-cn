---
title: 双正斜杠 （注释） (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7f6e05ac728f6e1a9dda94dfcb07d26309b3e1f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061674"
---
# <a name="double-slash-comment-dmx"></a>双斜杠 （注释） (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 您可以在数据挖掘扩展 (DMX) 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>Parameters  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>备注  
 只将 // 用于单行注释。 通过使用插入的注释 / / 由换行符分隔。  
  
 注释没有最大长度限制。  
  
 有关如何使用 DMX 中的不同种类注释的详细信息，请参阅[备注&#40;DMX&#41;](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>请参阅  
 [斜杠星型&#40;注释&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [-&#40;注释&#41; &#40;DMX&#41;摘要](../dmx/comment-dmx-summary.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
