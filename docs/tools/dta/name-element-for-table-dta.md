---
title: "表的名称元素 (DTA) | Microsoft Docs"
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
ms.assetid: 422a755f-ee52-4863-b1aa-f4ef1b8fd0bb
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# 表的名称元素 (DTA)
  指定表名以进行优化。  
  
## 语法  
  
```  
  
<Schema>  
    <Table>  
        <Name>...</Name>  
```  
  
## 元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**字符串**，长度为 1 到 255 个字符。|  
|**默认值**|无。|  
|**出现次数**|必需的。 每个 **Table** 元素一次。|  
  
## 元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[架构的表元素 (DTA)](../../tools/dta/table-element-for-schema-dta.md)|  
|**子元素**|无。|  
  
## 示例  
 有关使用示例，请参阅[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## 另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  