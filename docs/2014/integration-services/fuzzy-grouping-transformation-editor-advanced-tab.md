---
title: 模糊分组转换编辑器 （高级选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 074a3d460a04180a5cfce1406b546fb6a3a3986a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62893378"
---
# <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>模糊分组转换编辑器（“高级”选项卡）
  可以使用 **“模糊分组转换编辑器”** 对话框的 **“高级”** 选项卡，指定输入和输出列，设置相似性阈值以及定义分隔符。  
  
> [!NOTE]  
>  `Exhaustive`并`MaxMemoryUsage`模糊分组转换的属性中没有**模糊分组转换编辑器**，但可以通过使用设置**高级编辑器**. 有关这些属性的详细信息，请参阅 [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)的“模糊分组转换”部分。  
  
 若要了解有关模糊分组转换的详细信息，请参阅 [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md)。  
  
## <a name="options"></a>选项  
 **输入键列名**  
 指定包含每个输入行的唯一表示符的输出列名称。 `_key_in` 列包含的值可唯一标识每个行。  
  
 **输出键列名**  
 对于一组重复的行，指定包含其规范行的唯一标识符的输出列名称。 `_key_out` 列对应于规范数据行的 `_key_in` 值。  
  
 **相似性计分列名**  
 指定包含相似性得分的列的名称。 相似性得分是介于 0 和 1 之间的值，用于指示输入行与规范行的相似性。 得分越接近 1，行与规范行的匹配程度越高。  
  
 **相似性阈值**  
 使用滑块设置相似性阈值。 阈值越接近于 1，则行必须越近似，才能被认定为重复。 增大阈值可以提高匹配的速度，因为需要考虑的候选记录更少。  
  
 **标记分隔符**  
 转换提供了一组默认的分隔符用于对数据进行词汇切分，但是您可以根据需要通过编辑列表来添加或删除分隔符。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用模糊分组转换标识相似数据行](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
