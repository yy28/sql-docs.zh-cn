---
title: DropOnlyMode 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b4c0c0ce3c367ad557584bfbed222e93bc616d5f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171068"
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode 元素 (DTA)
  指定数据库引擎优化顾问在优化会话过程中只应考虑删除现有的索引、索引视图或分区。 如果指定了此优化选项，则不考虑任何新物理设计结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|可选。 可以使用仅一次为每个`TuningOptions`元素。 如果在指定了下列元素不能使用`TuningOptions`元素：<br /><br /> [FeatureSet 元素&#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [分区元素&#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> 将 [KeepExisting 元素 (DTA)](keepexisting-element-dta.md) 设置为 **ALL**|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素&#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 下面的示例演示`TuningOptions`部分中的数据库引擎优化顾问 XML 输入文件位置`DropOnlyMode`指定。 本例中，优化时间限定为 24 小时（1440 分钟），并且所有现有的聚集索引和非聚集索引将被删除：  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
