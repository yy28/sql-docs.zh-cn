---
title: "使用 URL 访问呈现报表历史记录快照 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "URL 访问 [Reporting Services], 报表历史记录"
  - "历史记录快照 [Reporting Services]"
  - "历史数据 [Reporting Services]"
  - "快照 [Reporting Services], URL 访问"
  - "快照 [Reporting Services], 呈现报表历史记录"
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# 使用 URL 访问呈现报表历史记录快照
  您可以通过提供 *rs:Snapshot* 参数并将其值设置为有效的快照 ID，基于报表历史记录快照呈现报表。 参数值采用 YYYY-MM-DDTHH:MM:SS 格式，该格式基于国际标准化组织 (ISO) 8601 标准。  
  
 如果省略此参数，则报表将根据报表服务器的报表执行和缓存管理选项设置呈现。 有关报表执行的详细信息，请参阅[设置报表处理属性](../reporting-services/report-server/set-report-processing-properties.md)。  
  
## 示例  
 下面的示例说明检索历史记录快照的 URL：  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## 另请参阅  
 [URL 访问 (SSRS)](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
  
  