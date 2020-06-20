---
title: StorageBoundInMB 元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- StorageBoundInMB element
ms.assetid: a8374910-bf68-4edb-b464-53a3a705e7f4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 12dad78b6094e940a926fbcde7147d66ca1e2dfe
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007597"
---
# <a name="storageboundinmb-element-dta"></a>StorageBoundInMB 元素 (DTA)
  指定数据库引擎优化顾问优化建议（索引和分区集）可用的最大空间 (MB)。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <StorageBoundInMB>...</ StorageBoundInMB >  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|`unsignedInt`，长度没有限制。|  
|**默认值**|无。|  
|**出现次数**|可选。 仅能对 `TuningOptions` 元素使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 (DTA)](tuningoptions-element-dta.md)|  
|**子元素**|无|  
  
## <a name="remarks"></a>备注  
 优化多个数据库时，建议对所有数据库都进行空间计算。 默认情况下，数据库引擎优化顾问会使用以下存储空间中较小的一个：  
  
-   当前原始数据大小的三倍，原始数据包含堆大小和表的聚集索引大小的总和。  
  
-   所有已附连磁盘驱动器的可用空间加上原始数据的大小。  
  
 默认存储大小不包括非聚集索引和索引视图。  
  
 如果为 `StorageBoundInMB` 元素指定的值超出了磁盘空间的实际大小，则数据库引擎优化顾问会返回一个错误消息，但继续进行优化。 优化完成之后，如果决定实现建议，则可增加磁盘空间。  
  
## <a name="example"></a>示例  
  
## <a name="description"></a>说明  
 以下代码示例说明如何将优化建议可以消耗的最大磁盘空间设置为 1500 MB：  
  
## <a name="code"></a>代码  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <StorageBoundInMB>1500</StorageBoundInMB>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
