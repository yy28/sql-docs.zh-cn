---
title: -（注释） (DMX) 摘要 |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- commenting characters
- double hyphens
- -- (comment character)
ms.assetid: 487b580b-5b81-4e52-8868-4fa809e4ef58
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 33c96340b0c020124ed995ca69284f81b44a5e28
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>注释  
 该运算符用于单行或嵌套的注释。 通过使用 -- 插入的注释由换行符分隔。  
  
 注释没有最大长度限制。  
  
 有关如何在 DMX 中使用不同类型的注释的详细信息，请参阅[注释&#40;DMX&#41;](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [正斜杠星型&#40;注释&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [双斜线&#40;注释&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
