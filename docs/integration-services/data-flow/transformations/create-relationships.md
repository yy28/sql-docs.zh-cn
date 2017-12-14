---
title: "创建关系 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.createrelationships.f1
ms.assetid: 6ebd305f-ffd2-4a1d-b24c-e28c151b94f5
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 651ad318f4bc55291eab79041c41167b9ee08e0d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="create-relationships"></a>创建关系
  可以使用 **“创建关系”** 对话框，编辑源列与在模糊查找转换编辑器、查找转换编辑器或字词查找转换编辑器中配置的查找表列之间的映射。  
  
> [!NOTE]  
>  通过字词查找转换编辑器调用“创建关系”对话框时，只显示“输入列”和“查找列”列表。  
  
 若要了解有关使用 **“创建关系”** 对话框的转换的详细信息，请参阅 [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)、 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)和 [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)。  
  
## <a name="options"></a>选项  
 **输入列**  
 从可用输入列的列表中进行选择。  
  
 **查找列**  
 从可用查找列的列表中进行选择。  
  
 **映射类型**  
 选择模糊匹配或完全匹配。  
  
 在使用模糊匹配时，如果行中所有具有模糊匹配类型的列都非常相似，则将视为重复的行。 若要从模糊匹配中获取更为准确的结果，可以指定一些列使用完全匹配来代替模糊匹配。 例如，如果知道特定列中没有错误或不存在不一致的情况，则可以对该列指定完全匹配，以便只有在此列中包含相同值的行才会视为可能重复。 这样可以提高其他列模糊匹配的准确性。  
  
 **比较标志**  
 有关字符串比较选项的信息，请参阅 [比较字符串数据](../../../integration-services/data-flow/comparing-string-data.md)。  
  
 **最低相似性**  
 使用滑块在列级别设置相似性阈值。 该值越接近 1，查找值与源值必须越相似，才能视为匹配。 增大阈值可以提高匹配的速度，因为需要考虑的候选记录更少。  
  
 **相似性输出别名**  
 为包含所选列相似性得分的新输出列指定名称。 如果将该值保留为空，将不会创建输出列。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [模糊查找转换编辑器（“列”选项卡）](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [查找转换编辑器（“列”页）](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [字词查找转换编辑器（“字词查找”选项卡）](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-term-lookup-tab.md)  
  
  
