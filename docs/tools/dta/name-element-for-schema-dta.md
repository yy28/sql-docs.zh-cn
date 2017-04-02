---
title: "架构的名称元素 (DTA) | Microsoft Docs"
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
  - "名称元素"
ms.assetid: 014e4854-fed2-454b-8557-5f7c5bb6b17a
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# 架构的名称元素 (DTA)
  包含架构的名称。  
  
## 语法  
  
```  
  
<Database>  
...code removed here  
    <Schema>  
        <Name>...</Name>  
```  
  
## 元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**string**，介于 1 到 255 个字符之间|  
|**默认值**|无。|  
|**出现次数**|要求每个 **架构** 元素出现一次。|  
  
## 元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[数据库的架构元素 (DTA)](../../tools/dta/schema-element-for-database-dta.md)|  
|**子元素**|无。|  
  
## 示例  
 有关此元素的使用示例，请参阅[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## 另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  