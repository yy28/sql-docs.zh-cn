---
title: 聚合转换编辑器 （高级选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregationtransformation.advanced.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: 186a9736-2554-40a0-9cb2-877a8db5fde8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 605a92e00b21d64679076fabcb41068b94921779
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771933"
---
# <a name="aggregate-transformation-editor-advanced-tab"></a>聚合转换编辑器（“高级”选项卡）
  可以使用 **“聚合转换编辑器”** 对话框的 **“高级”** 选项卡设置组件属性，指定聚合以及设置输入和输出列的属性。  
  
> [!NOTE]  
>  对于键计数、键范围、非重复键计数和非重复键范围的选项来说，如果是在“高级”选项卡中指定的，则会应用于组件级；如果是在“聚合”选项卡的高级显示部分中指定的，则会应用于输出级；而如果是在“聚合”选项卡底部的列列表中指定的，则会应用于列级。  
>   
>  在聚合转换中， **“键”** 和 **“键范围”** 是指期望 **“分组依据”** 操作产生的组数。 **“非重复键计数”** 和 **“非重复键数范围”** 是指期望 **“非重复计数”** 操作产生的非重复值的数量。  
  
 若要了解有关聚合转换的详细信息，请参阅 [Aggregate Transformation](data-flow/transformations/aggregate-transformation.md)。  
  
## <a name="options"></a>选项  
 **“键范围”**  
 根据需要，可以指定聚合所需的键的大致数目。 转换将使用此信息优化其初始缓存大小。 默认情况下，此选项的值为 **“未指定”**。 如果同时指定了 **“键范围”** 和 **“键数”** ，则 **“键数”** 优先。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|“未指定”|不使用 **“键范围”** 属性。|  
|Low|聚合可以写入大约 500,000 个键。|  
|Medium|聚合可以写入大约 5,000,000 个键。|  
|High|聚合可以写入 25,000,000 个以上的键。|  
  
 **“键数”**  
 根据需要，可以指定聚合所需的键的精确数目。 转换将使用此信息优化其初始缓存大小。 如果同时指定了 **“键范围”** 和 **“键数”** ，则 **“键数”** 优先。  
  
 **“非重复键数范围”**  
 根据需要，可以指定聚合能够写入的非重复值的大致数目。 默认情况下，此选项的值为 **“未指定”**。 如果同时指定了 **“非重复键数范围”** 和 **“非重复键计数”** ，则 **“非重复键计数”** 优先。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|“未指定”|不使用 CountDistinctScale 属性。|  
|Low|聚合可以写入大约 500,000 个非重复值。|  
|Medium|聚合可以写入大约 5,000,000 个非重复值。|  
|High|聚合可以写入 25,000,000 个以上的非重复值。|  
  
 **“非重复键计数”**  
 根据需要，可以指定聚合能够写入的非重复值的精确数目。 如果同时指定了 **“非重复键数范围”** 和 **“非重复键计数”** ，则 **“非重复键计数”** 优先。  
  
 **自动扩展系数**  
 使用一个 1 到 100 之间的值指定在聚合过程中内存可扩展的百分比。 默认情况下，此选项的值为 **25%**。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [聚合转换编辑器（“聚合”选项卡）](../../2014/integration-services/aggregate-transformation-editor-aggregations-tab.md)   
 [使用聚合转换来聚合数据集中的值](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
