---
title: "服务器的数据库元素 (DTA) | Microsoft Docs"
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
  - "数据库元素"
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# 服务器的数据库元素 (DTA)
  指定特定服务器上要优化的数据库。  
  
## 语法  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## 元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无。|  
|默认值|无。|  
|出现次数|对于每个 **Server** 元素需要使用一次或多次。|  
  
## 元素关系  
  
|关系|元素|  
|------------------|--------------|  
|父元素|[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)|  
|子元素|[数据库的名称元素 (DTA)](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [数据库的架构元素 (DTA)](../../tools/dta/schema-element-for-database-dta.md)|  
  
## 注释  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseDetailsTypecomplexType**。 请不要将此 **Database** 元素与根级父元素为 **Configuration** 元素的元素相混淆。 有关详细信息，请参阅[用于配置的数据库元素 (DTA)](../../tools/dta/database-element-for-configuration-dta.md)。  
  
## 示例  
 有关**数据库**元素的用法示例，请参阅[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## 另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  