---
description: -- (注释)  (DMX) 摘要
title: -- (注释)  (DMX) 摘要 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 260a3f5c8a6d1badb90349396db6f2b716380aa7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431089"
---
# <a name="---comment-dmx-summary"></a>-- (注释)  (DMX) 摘要
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 您可以在数据挖掘扩展 (DMX) 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>参数  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>备注  
 该运算符用于单行或嵌套的注释。 通过使用 -- 插入的注释由换行符分隔。  
  
 注释没有最大长度限制。  
  
 有关如何在 DMX 中使用不同种类的注释的详细信息，请参阅 [&#40;dmx&#41;的注释 ](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [斜杠星形 &#40;注释&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [双斜线 &#40;注释&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
