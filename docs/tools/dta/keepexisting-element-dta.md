---
title: "KeepExisting 元素 (DTA) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5eca95f9df364166a798fee014cfad4521c87ae4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="keepexisting-element-dta"></a>KeepExisting 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]指定数据库引擎优化顾问生成其建议时必须保留的物理设计结构 （索引、 索引的视图或分区）。  
  
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
|**数据类型和长度**|**string**，服务器强制执行的长度限制。|  
|**允许的值**|**NONE**<br /> 无现有结构。<br /><br /> **ALL**<br /> 所有现有结构。<br /><br /> **ALIGNED**<br /> 所有分区对齐结构。<br /><br /> **CL_IDX**<br /> 表中的所有聚集索引。<br /><br /> **IDX**<br /> 表中的所有聚集索引和非聚集索引。<br /><br /> 只能将这些值中的一个用于此元素。|  
|**默认值**|无。|  
|**出现次数**|可选。 对于每个 **TuningOptions** 元素只能使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 (DTA)](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关此元素的使用示例，请参阅[简单 XML 输入文件示例 (DTA)](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
