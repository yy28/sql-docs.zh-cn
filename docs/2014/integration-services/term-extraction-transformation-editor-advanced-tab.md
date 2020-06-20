---
title: 字词提取转换编辑器（"高级" 选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6c783a06d5d5518639e6368f5c1eb572e60206b5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962257"
---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>字词提取转换编辑器（“高级”选项卡）
  可以使用 **“字词提取转换编辑器”** 对话框的 **“高级”** 选项卡，指定频率、长度等提取属性以及指定是提取字词还是提取短语。  
  
 若要了解有关字词提取转换的详细信息，请参阅 [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md)。  
  
## <a name="options"></a>选项  
 **名词**  
 指定转换仅提取各个名词。  
  
 **名词短语**  
 指定转换仅提取名词短语。  
  
 **名词和名词短语**  
 指定转换既提取名词也提取名词短语。  
  
 **频率**  
 指定分数为字词的频率。  
  
 **TFIDF**  
 指定分数为字词的 TFIDF 值。 TFIDF 分数是字词频率和文档频率倒数的乘积，其定义如下：TFIDF of a Term T = (frequency of T) * log( (#rows in Input) / (#rows having T) )。  
  
 **频率阈值**  
 指定某个词或短语必须出现多少次以后才对其进行提取。 默认值为 2。  
  
 **字词的最大长度**  
 指定短语的最大长度（字）。 此选项仅影响名词短语。 默认值为 12。  
  
 **使用区分大小写的字词提取**  
 指定是否将提取设置为区分大小写。 默认为 `False`。  
  
 **配置错误输出**  
 使用[“配置错误输出” ](../../2014/integration-services/configure-error-output.md) 对话框可以为导致错误的行指定错误处理方式。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [字词提取转换编辑器 &#40;字词提取选项卡&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [字词提取转换编辑器 &#40;排除选项卡&#41;](../../2014/integration-services/term-extraction-transformation-editor-exclusion-tab.md)   
 [字词查找转换](data-flow/transformations/lookup-transformation.md)  
  
  
