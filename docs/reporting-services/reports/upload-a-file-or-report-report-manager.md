---
title: "上载文件或报表（报表管理器） | Microsoft Docs"
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
  - "发布报表 [Reporting Services], 上载文件"
  - "报表 [Reporting Services], 发布"
  - "上载报表 [Reporting Services]"
  - "上载文件 [Reporting Services]"
  - "文件 [Reporting Services], 上载"
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# 上载文件或报表（报表管理器）
  报表管理器提供上载功能，因而您可以将报表、模型以及其他文件添加到报表服务器而不必从客户端应用程序发布这些项。 从文件系统上载的文件会存储为报表服务器上的项。 所上载的文件类型决定存储方式：  
  
-   .rdl 文件存储为报表。  
  
-   .smdl 文件存储为报表模型。  
  
-   包括共享数据源 (.rds) 文件在内的所有其他文件都上载为资源。 报表服务器不会处理资源，但是如果报表服务器支持 MIME 文件类型，则可以通过报表管理器来查看资源。  
  
### 上载文件或报表  
  
1.  启动[报表管理器（SSRS 本机模式）](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)。  
  
2.  在报表管理器中，导航到 **“内容”** 页。 导航到要向其中添加项的文件夹。  
  
3.  单击 **“上载文件”**。  
  
4.  单击 **“浏览”** 以选择要上载的文件。 可以上载报表定义文件、图像、文档或任何要在报表服务器上可用的文件。  
  
5.  键入新项的名称。 项名称可以包括空格，但不能包括保留字符: ; ? : @ & = + , $ / * \< > |。  
  
6.  若要用新项替换现有项，请选择 **“如果该项已存在，则覆盖该项”**。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另请参阅  
 [创建、删除或修改共享数据源（报表管理器）](../Topic/Create,%20Delete,%20or%20Modify%20a%20Shared%20Data%20Source%20\(Report%20Manager\).md)   
 [“内容”页（报表管理器）](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [“上传文件”页（报表管理器）](../Topic/Upload%20File%20Page%20\(Report%20Manager\).md)   
 [将文件上载到文件夹](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  