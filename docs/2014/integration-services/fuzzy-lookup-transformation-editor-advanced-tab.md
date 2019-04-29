---
title: 模糊查找转换编辑器 （高级选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 0a2919be-2ea7-4c06-82b8-0ffad5f0dd83
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0739bb7100e61147e0ba35cb1cc75b1367634924
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62893219"
---
# <a name="fuzzy-lookup-transformation-editor-advanced-tab"></a>模糊查找转换编辑器（“高级”选项卡）
  可以使用 **“模糊查找转换编辑器”** 对话框的 **“高级”** 选项卡设置模糊查找的参数。  
  
 若要了解有关模糊查找转换的详细信息，请参阅 [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md)。  
  
## <a name="options"></a>选项  
 **每次查找输出的最大匹配数**  
 指定为每个输入行返回的最大匹配转换数。 默认值为 **1**。  
  
 **相似性阈值**  
 使用滑块在组件级别设置相似性阈值。 该值越接近 1，查找值与源值的相似性必须越接近，才能视为匹配。 由于需要考虑的候选记录更少，因此增加阈值可以提高匹配的速度。  
  
 **标记分隔符**  
 指定转换用来对列值进行词汇切分的分隔符。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [模糊查找转换编辑器（“引用表”选项卡）](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [模糊查找转换编辑器（“列”选项卡）](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)  
  
  
