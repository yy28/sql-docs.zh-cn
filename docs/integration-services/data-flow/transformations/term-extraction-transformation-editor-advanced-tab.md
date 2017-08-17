---
title: "字词提取转换编辑器 （高级选项卡） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 605085b59357a98011c801f8aa4675e89c3cd8a9
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>字词提取转换编辑器（“高级”选项卡）
  可以使用 **“字词提取转换编辑器”** 对话框的 **“高级”** 选项卡，指定频率、长度等提取属性以及指定是提取字词还是提取短语。  
  
 若要了解有关字词提取转换的详细信息，请参阅 [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)。  
  
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
 指定分数为字词的 TFIDF 值。 TFIDF 分数是字词频率和文档频率倒数的乘积，其定义如下：TFIDF of a Term T = (frequency of T) * log( (#rows in Input) / (#rows having T) )  
  
 **频率阈值**  
 指定某个词或短语必须出现多少次以后才对其进行提取。 默认值为 2。  
  
 **字词的最大长度**  
 指定短语的最大长度（字）。 此选项仅影响名词短语。 默认值为 12。  
  
 **使用区分大小写的字词提取**  
 指定是否将提取设置为区分大小写。 默认值为 **False**。  
  
 **配置错误输出**  
 使用 [配置错误输出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框可以为导致错误的行指定错误处理方式。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [字词提取转换编辑器 &#40;字词提取选项卡 &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)   
 [字词提取转换编辑器 &#40;排除选项卡 &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-exclusion-tab.md)   
 [字词查找转换](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
  
