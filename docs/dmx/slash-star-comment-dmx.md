---
title: 斜杠星形（注释）（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5d0b929ba60915f116d9ff6843b4f20b3105a7ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67942848"
---
# <a name="slash-star-comment-dmx"></a>斜杠星形（注释）（DMX）
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不应执行的文本字符串。 服务器不会计算注释字符/* 和\*/之间的文本。 您可以在数据挖掘扩展 (DMX) 语句中嵌入注释，将其加在代码行末尾，或者单独插入一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>参数  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>备注  
 多行的注释必须用 /* 和 \*/ 指明。  
  
 注释没有最大长度限制。  
  
 有关如何在 DMX 中使用不同种类的注释的详细信息，请参阅[&#40;dmx&#41;的注释](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [双斜线 &#40;注释&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [--&#40;注释&#41; &#40;DMX&#41; 摘要](../dmx/comment-dmx-summary.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
