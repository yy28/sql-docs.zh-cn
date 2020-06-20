---
title: FeatureSet 元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 79cb42654619ea3802d513fcf63df879833e48f1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048412"
---
# <a name="featureset-element-dta"></a>FeatureSet 元素 (DTA)
  包含数据库引擎优化顾问在分析中使用的物理设计结构（索引或索引视图）。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|`string`，无最大长度。|  
|**允许的值**|**IDX_IV**<br /> 索引和索引视图。<br /><br /> **IDX**<br /> 仅限索引。<br /><br /> **IV**<br /> 仅限索引视图。<br /><br /> **NCL_IDX**<br /> 仅限非聚集索引。<br /><br /> 将这些值中的一个值用于此元素。|  
|**默认值**|**IDX**|  
|**出现次数**|除非使用了 `TuningOptions` 元素，否则对每个 `DropOnlyMode` 元素仅需要一次。 如果使用 `DropOnlyMode`，则无法使用 `FeatureSet`。 这两种元素是互相排斥的。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 (DTA)](tuningoptions-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关此元素的使用示例，请参阅[简单 XML 输入文件示例 (DTA)](simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
