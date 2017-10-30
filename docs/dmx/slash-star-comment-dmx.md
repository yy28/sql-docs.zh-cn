---
title: "正斜杠星型 （注释） (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- commenting characters
- forward slash-asterisk character pairs
- /*...*/ (comment)
ms.assetid: 163976cc-aa47-4eda-bd98-03c1a397f80e
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5bfaadd08f5a9aba145c754f281cf1d2c8e38496
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="slash-star-comment-dmx"></a>斜杠星型 （注释） (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 服务器不会计算之间的注释字符的文本 / * 和\*/。 您可以在数据挖掘扩展 (DMX) 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>Parameters  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>備註  
 必须由指示多行注释 / * 和\*/。  
  
 注释没有最大长度限制。  
  
 有关如何在 DMX 中使用不同类型的注释的详细信息，请参阅[注释 &#40; DMX &#41;](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [双斜线 &#40;注释 &#41;&#40; DMX &#41;](../dmx/double-slash-comment-dmx.md)   
 [-&#40;注释 &#41;&#40; DMX &#41;摘要](../dmx/comment-dmx-summary.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

