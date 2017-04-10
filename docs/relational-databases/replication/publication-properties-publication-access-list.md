---
title: "发布属性，发布访问列表 | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.publicationaccesslist.f1"
ms.assetid: 9587bb9e-c66c-4e70-8171-09b943ec2d50
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 发布属性，发布访问列表
   **发布访问列表** 页 **发布属性** 对话框中，您可以添加和从发布访问列表 (PAL) 中删除登录名、 帐户和组。 PAL 是用于保护发布服务器的主要机制。 创建发布时，复制将为该发布创建 PAL。 PAL 的功能类似于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 访问控制列表，PAL 包含被授予该发布的访问权的登录名、帐户和组的列表。  
  
 当订阅服务器连接到发布服务器或分发服务器并请求访问发布时，订阅服务器的登录名将与 PAL 中的身份验证信息进行比较。 这样，通过防止客户端工具使用发布服务器和分发服务器登录名在发布服务器上直接进行修改，从而为发布服务器提供额外的安全性。 有关详细信息，请参阅 [安全发布服务器](../../relational-databases/replication/security/secure-the-publisher.md)。  
  
## 选项  
 **添加**  
 将新项添加到列表。 只能添加那些在发布服务器和分发服务器上均已定义的登录名、帐户或组名称。 如果使用域帐户或在两个服务器上都已创建本地帐户，则这些信息在两个服务器上均已定义。  
  
 **删除**  
 从列表中删除所选项。  
  
 **全部删除**  
 从列表中删除所有项。  
  
## 另请参阅  
 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  