---
title: 模糊分组转换编辑器（"列" 选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.columns.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a97225797380294968f1af595f1299e478d548d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058359"
---
# <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>模糊分组转换编辑器（“列”选项卡）
  可以使用 **“模糊分组转换编辑器”** 对话框的 **“列”** 选项卡，指定用于对带有重复值的行进行分组的列。  
  
 若要了解有关模糊分组转换的详细信息，请参阅 [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md)。  
  
## <a name="options"></a>选项  
 **可用输入列**  
 从此列表中选择用于对带有重复值的行进行分组的输入列。  
  
 **名称**  
 查看可用输入列的名称。  
  
 **传递**  
 选择是否在转换的输出中包含输入列。 用于分组的所有列将自动复制到输出中。 通过选中此列可以包含其他列。  
  
 **输入列**  
 选择先前在“可用输入列”**** 列表中选中的一个输入列。  
  
 **输出别名**  
 为相应的输出列输入一个描述性名称。 默认情况下，输出列名称与输入列名称相同。  
  
 **组输出别名**  
 为包含分组重复项的规范值的列输入一个描述性名称。 此输出列的默认名称是在输入列名称后面追加 _clean。  
  
 **匹配类型**  
 选择模糊匹配或完全匹配。 在指定了模糊匹配类型的所有列中，如果某些行足够相似，则会将这些行视为重复。 如果还对某些列指定了完全匹配，则只会将在完全匹配列中包含相同值的行视为可能重复。 因此，如果知道特定列中没有错误或不存在不一致的情况，则可以对该列指定完全匹配以提高其他列模糊匹配的准确性。  
  
 **最低相似性**  
 使用滑块在联接级别设置相似性阈值。 该值越接近 1，查找值与源值的相似性必须越接近，才能视为匹配。 由于需要考虑的候选记录更少，因此增加阈值可以提高匹配的速度。  
  
 **相似性输出别名**  
 为包含所选联接相似性得分的新输出列指定名称。 如果将该值保留为空，将不会创建输出列。  
  
 **数字**  
 指定比较列数据时前导数字和尾随数字的重要性。 例如，如果前导数字重要，则“123 Main Street”将不会与“456 Main Street”分组在一起。  
  
|值|说明|  
|-----------|-----------------|  
|**但**|前导数字和尾随数字都不重要。|  
|**前导**|只有前导数字重要。|  
|**加**|只有尾随数字重要。|  
|**LeadingAndTrailing**|前导数字和尾随数字都重要。|  
  
 **比较标志**  
 有关字符串比较选项的信息，请参阅 [比较字符串数据](data-flow/comparing-string-data.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用模糊分组转换标识相似数据行](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
