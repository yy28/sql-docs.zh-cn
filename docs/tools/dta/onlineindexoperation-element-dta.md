---
title: "OnlineIndexOperation 元素 (DTA) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "OnlineIndexOperation 元素"
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# OnlineIndexOperation 元素 (DTA)
  指定是否可联机创建数据库引擎优化顾问建议的索引、索引视图或分区。  
  
## 语法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## 元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**string**，无最大长度。|  
|**允许的值**|**OFF**<br /> 建议的物理设计结构都无法联机创建。<br /><br /> **ON**<br /> 所有建议的物理设计结构都可以联机创建。<br /><br /> **MIXED**<br /> 数据库引擎优化顾问会尝试建议可以联机创建的物理设计结构。<br /><br /> 将这些值中的一个值用于此元素。 如果联机创建索引，则将向其对象定义中追加 **ONLINE = ON** 关键字。|  
|**默认值**|无。|  
|**出现次数**|可选。 如果使用 **TuningOptions** 元素，则只能使用一次。|  
  
## 元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 (DTA)](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|无。|  
  
## 示例  
 有关此元素的使用示例，请参阅[简单 XML 输入文件示例 (DTA)](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## 另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  