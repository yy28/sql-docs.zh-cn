---
title: "服务器的名称元素 (DTA) | Microsoft Docs"
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
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# 服务器的名称元素 (DTA)
  包含要优化的数据库所在服务器的名称。  
  
## 语法  
  
```  
  
...code removed here...  
<Server>  
    <Name>...</Name>  
```  
  
## 元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**字符串**，长度为 1 到 255 个字符。|  
|**默认值**|无。|  
|**出现次数**|每个 **服务器** 元素必须出现一次。|  
  
## 元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)|  
|**子元素**|无。|  
  
## 示例  
 有关如何使用该 **Name** 元素的示例，请参阅[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## 另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  