---
title: KeepExisting 元素 (DTA) |Microsoft Docs
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
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8691e57b9750447b1740c79337b75500febd9549
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070737"
---
# <a name="keepexisting-element-dta"></a>KeepExisting 元素 (DTA)
  指定数据库引擎优化顾问在生成建议时必须保留的物理设计结构（索引、索引视图或分区）。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|`string`，服务器强制执行的长度限制。|  
|**允许的值**|**NONE**<br /> 无现有结构。<br /><br /> **ALL**<br /> 所有现有结构。<br /><br /> **ALIGNED**<br /> 所有分区对齐结构。<br /><br /> **CL_IDX**<br /> 表中的所有聚集索引。<br /><br /> **IDX**<br /> 表中的所有聚集索引和非聚集索引。<br /><br /> 只能将这些值中的一个用于此元素。|  
|**默认值**|无。|  
|**出现次数**|可选。 可以使用仅一次为每个`TuningOptions`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素&#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关此元素的使用示例，请参阅[简单 XML 输入文件示例 (DTA)](simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
