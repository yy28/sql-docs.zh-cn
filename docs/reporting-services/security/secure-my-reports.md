---
title: "保护“我的报表” | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "拒绝访问“我的报表”文件夹"
  - "专用文件夹 [Reporting Services]"
  - "用户工作区 [Reporting Services]"
  - "安全性 [Reporting Services], “我的报表”文件夹"
  - "“我的报表”文件夹 [Reporting Services]"
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
caps.latest.revision: 34
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 34
---
# 保护“我的报表”
  “我的报表”功能为使用报表提供了一个由用户管理的工作区。 为了发挥“我的报表”文件夹应有的作用，该文件夹与其他普通文件夹相比，需要限制条件较少的权限。 只有在其他文件夹中查看和运行报表的权限的用户可能需要一组扩展的权限来管理其“我的报表”文件夹及其所拥有的内容。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供专用于此用途的角色分配和角色定义。  
  
> [!NOTE]  
>  “我的报表”只适用于报表管理器。 该文件夹在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中不可用。  
  
## “我的报表”的角色分配  
 “我的报表”的角色分配中的元素都是预先设置好的，对于激活“我的报表”文件夹的每个用户，将自动为其创建角色分配。 对于广泛使用“我的报表”的单位而言，让报表服务器自动分配安全性尤其有用，因为管理员不必为每一个“我的报表”用户授予访问权限。  
  
 “我的报表”角色分配由以下元素组成：   
  
-   用户的“我的报表”文件夹，位于“用户文件夹\\<用户名\>\我的报表”文件夹下。  
  
-   用户帐户，在激活“我的报表”文件夹时确定。 当用户单击报表管理器中的“我的报表”文件夹时，或将报表从报表设计器发布到“我的报表”文件夹时，将激活一个文件夹。 当用户请求“我的报表”链接的属性时，也将激活此文件夹。  
  
-   “我的报表”的预定义角色定义  
  
## “我的报表”的角色定义  
 “我的报表”角色定义包含支持对“我的报表”文件夹的内容进行管理的任务。  “我的报表”角色设计作为单一用途的角色。 虽然您可以将该角色用于任何项级安全策略，但最好不要这样做，以尽量避免为满足其他文件夹要求而修改该角色。 为“我的报表”功能保留“我的报表”角色有助于维护一致的用户体验。   
  
 默认情况下，只有报表服务器管理员才可以修改“我的报表”角色。  您可以通过更改“我的报表”角色所包含的任务来自定义“我的报表”角色。  您还可以替换其他角色。  
  
## 拒绝访问“我的报表”  
 可以通过以下方式阻止用户访问“我的报表”：  
  
-   在“站点设置”页上禁用“我的报表”。 有关详细信息，请参阅[启用和禁用“我的报表”](../../reporting-services/report-server/enable-and-disable-my-reports.md)。  
  
-   删除“我的报表”角色中的所有任务。   
  
 禁用“我的报表”后，将从报表管理器中删除指向“我的报表”文件夹的链接。 支持“我的报表”的基础文件夹结构（即用户文件夹及其子文件夹）仍然可用，如果用户知道文件夹路径，仍可对其进行访问。 删除“我的报表”角色中的任务可以确保禁止对该文件夹的访问。   
  
## 另请参阅  
 [保护报表和资源](../../reporting-services/security/secure-reports-and-resources.md)   
 [保护文件夹](../../reporting-services/security/secure-folders.md)   
 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  