---
title: "Banner 元素 (ssbdiagnose) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "banner 元素"
  - "XML 输出文件格式 [ssbdiagnose], banner 元素"
  - "ssbdiagnose"
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Banner 元素 (ssbdiagnose)
  标识生成 **ssbdiagnose** 输出 XML 文件的实用工具。  
  
## 语法  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## 元素属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|**title**|标识生成 **ssbdiagnose** XML 输出文件的实用工具。|  
|**product**|标识生成 **ssbdiagnose** XML 输出文件的产品。|  
|**version**|标识生成 XML 输出文件的实用工具的版本。|  
  
## 元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|每个 **ssbdiagnose** 输出 XML 文件出现一次。|  
  
## 元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DiagnosticInformation 元素 (ssbdiagnose)](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**子元素**|无。|  
  
## 示例  
 这是一个 Banner 元素的示例。  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## 另请参阅  
 [ssbdiagnose 实用工具 (Service Broker)](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  