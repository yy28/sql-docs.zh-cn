---
title: DropOnlyMode 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f75d3a4c293ebcb2f91c39df4cb1c008601dcde2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62857096"
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  指定数据库引擎优化顾问在优化会话过程中只应考虑删除现有的索引、索引视图或分区。 如果指定了此优化选项，则不考虑任何新物理设计结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>元素特征  
 **数据类型和长度**  
  
 **默认值**  
  
 **出现次数**：可选。 对于每个 **TuningOptions** 元素只能使用一次。 如果在 **TuningOptions** 元素中指定了下列元素，则不能使用此元素：  
  
-   [FeatureSet 元素 (DTA)](../../tools/dta/featureset-element-dta.md)  
  
-   [分区元素 (DTA)](../../tools/dta/partitioning-element-dta.md)  
  
-   将 [KeepExisting 元素 (DTA)](../../tools/dta/keepexisting-element-dta.md) 设置为 **ALL**  
  
## <a name="element-relationships"></a>元素关系  
 **父元素**：[TuningOptions 元素 (DTA)](../../tools/dta/tuningoptions-element-dta.md)  
  
 **子元素**  
  
## <a name="example"></a>示例  
 以下示例说明数据库引擎优化顾问 XML 输入文件的 **TuningOptions** 部分，其中指定了 **DropOnlyMode** 。 本例中，优化时间限定为 24 小时（1440 分钟），并且所有现有的聚集索引和非聚集索引将被删除：  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
