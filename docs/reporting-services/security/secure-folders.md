---
title: "保护文件夹 | Microsoft Docs"
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
  - "高安全性文件夹 [Reporting Services]"
  - "低安全性文件夹"
  - "文件夹 [Reporting Services], 安全性"
  - "安全性 [Reporting Services], 文件夹"
ms.assetid: 0fd91f77-0143-476b-9af0-87293be78e44
caps.latest.revision: 34
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 34
---
# 保护文件夹
  文件夹的安全性是保护报表服务器中所有内容的基础。 由于安全性在整个文件夹结构中是可继承的，因此您可以将文件夹层次结构中或大或小的不同部分指定为允许某些类型的访问。  
  
 安全性较高的文件夹可用来存储机密报表或用作临时区域；例如，在将报表移到最终位置之前，可以在某个文件夹中测试这些报表。 若要控制对此区域的访问，您可以定义一个只允许报表作者添加和删除项的角色分配，并定义一个允许测试人员运行报表但不能添加或删除项的角色分配。 由于这些角色分配是明确地为测试人员和报表作者定义的，因此其他用户不能访问该文件夹（本地系统管理员除外）。  
  
 安全性较低的文件夹可用来存储希望易于访问的报表。  
  
 文件夹安全性构成了项级安全性的基础，其基点是报表服务器文件夹层次结构的根节点（即主文件夹）。 由于安全性是可继承的，因此，建议您对主文件夹设置限制相当严格的安全策略。 在主文件夹角色分配中使用“浏览者”角色，即可通过提供只读访问来做到这一点。  
  
## 任务和文件夹访问权限  
 在为文件夹创建角色分配时，请考虑下表中列出的任务：  
  
|选择此任务|授予以下操作权限|  
|----------------------|---------------------------|  
|查看文件夹|查看文件夹的层次结构和只读属性（指示文件夹的创建时间与修改时间）。<br /><br /> 除非将用户分配到的角色中还包括“查看报表”、“查看模型”、“查看资源”和“查看数据源”任务，否则用户无法查看文件夹中的项。|  
|管理文件夹|查看文件夹属性、更改名称或说明，或将文件夹移到另一位置。 此任务允许用户创建文件夹。|  
|管理报表|将报表从文件系统添加到文件夹，以及将报表从报表设计器发布到报表服务器。|  
|管理数据源|向文件夹中添加新的共享数据源项，以及更改现有的共享数据源。|  
|设置项的安全性|创建和修改控制文件夹访问权限的角色分配。 此任务必须与“查看文件夹”或“管理文件夹”任务一起使用。 否则，此任务不会有任何作用，因为用户无法选择项。|  
  
## 另请参阅  
 [保护报表和资源](../../reporting-services/security/secure-reports-and-resources.md)   
 [保护共享数据源项](../../reporting-services/security/secure-shared-data-source-items.md)   
 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  