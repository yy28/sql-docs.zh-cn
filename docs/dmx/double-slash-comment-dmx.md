---
title: 双正斜杠 （注释） (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- double forward slashes
- commenting characters
- // (comment)
ms.assetid: c2ab9ca1-9fc9-4162-97f9-a9433d189220
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 72d91543e9e384f48f4e1220e5926fedbb5787f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="double-slash-comment-dmx"></a>双斜线 （注释） (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 您可以在数据挖掘扩展 (DMX) 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>Parameters  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>注释  
 只将 // 用于单行注释。 通过使用插入的批注，/ / 由换行符分隔。  
  
 注释没有最大长度限制。  
  
 有关如何在 DMX 中使用不同类型的注释的详细信息，请参阅[注释&#40;DMX&#41;](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [正斜杠星型&#40;注释&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [-&#40;注释&#41; &#40;DMX&#41;摘要](../dmx/comment-dmx-summary.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
