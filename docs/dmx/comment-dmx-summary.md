---
title: -（注释） (DMX) 摘要 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: be2fc3e82e1da18a12af4bc4756811225e85a280
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031445"
---
# <a name="---comment-dmx-summary"></a>-（注释） (DMX) 摘要
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 您可以在数据挖掘扩展 (DMX) 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parameters  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>Remarks  
 该运算符用于单行或嵌套的注释。 通过使用 -- 插入的注释由换行符分隔。  
  
 注释没有最大长度限制。  
  
 有关如何使用 DMX 中的不同种类注释的详细信息，请参阅[备注&#40;DMX&#41;](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>请参阅  
 [斜杠星型&#40;注释&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [双斜杠&#40;注释&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
