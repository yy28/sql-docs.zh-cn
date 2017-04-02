---
title: "分发服务器属性，发布服务器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configdistwizard.distproperties.publishers.f1"
helpviewer_keywords: 
  - "“分发服务器属性”对话框"
ms.assetid: 31c81898-11ca-4d2f-afea-2fbc71e19ce4
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 分发服务器属性，发布服务器
  可以使用 **“分发服务器属性”** 对话框的 **“发布服务器”** 页，允许发布服务器使用此分发服务器。 还可以设置与这些发布服务器关联的属性。 请注意，允许发布服务器将此服务器用作其远程分发服务器的同时，并不会使该服务器成为发布服务器。 必须连接到发布服务器，对其进行配置以用于发布，并选择此服务器作为分发服务器。 您可以通过新建发布向导配置发布服务器并选择分发服务器。  
  
## 选项  
 **发布服务器**  
 选择允许使用此分发服务器的服务器。 单击属性按钮 **（...）** 发布服务器可以查看和设置其他属性旁边。  
  
 **添加**  
 如果未列出您想要允许的服务器，请单击 **添加** 添加 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器或 Oracle 发布服务器到可用的发布服务器的列表。 如果添加的服务器是使用此分发服务器作为远程分发服务器的第一个服务器，则系统将会提示您提供管理链接密码。  
  
 **管理链接密码**  
 用来指定或在发布服务器和远程分发服务器上使用之间建立的连接复制的密码更新 **distributor_admin** 登录名︰  
  
-   如果分发服务器仅用作本地分发服务器，则会随机生成并自动配置此密码。  
  
-   如果分发服务器已具有远程发布服务器，则密码已在此页上或配置分发向导的 **“分发服务器密码”** 页上提供。  
  
-   如果为此分发服务器启用第一个远程发布服务器，则系统将会提示您输入密码。  
  
 分发服务器安全性的更多信息，请参阅 [安全分发服务器](../../relational-databases/replication/security/secure-the-distributor.md)。  
  
## 另请参阅  
 [配置分发](../../relational-databases/replication/configure-distribution.md)   
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  