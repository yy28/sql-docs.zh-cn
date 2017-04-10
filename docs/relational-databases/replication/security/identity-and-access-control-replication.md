---
title: "标识和访问控制（复制） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "访问控制 [SQL Server 复制]"
  - "安全性 [SQL Server 复制], 标识和访问控制"
  - "身份验证 [SQL Server 复制]"
  - "标识 [复制]"
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# 标识和访问控制（复制）
  身份验证是依据实体 （通常在此上下文中的计算机） 验证另一实体，也称为的过程 *主体*, ，（通常是另一计算机或用户） 是谁或声称要。 授权是给予通过身份验证的主体对资源（例如，文件系统中的文件或数据库中的表）的访问权限的过程。  
  
 复制安全性使用身份验证和授权，来控制对复制数据库对象和涉及复制处理的计算机及代理的访问。 这是通过三种机制实现的：  
  
-   代理安全性  
  
     用复制代理安全模式可以对复制代理运行和建立连接所用的帐户进行精细粒度的控制。 有关代理安全模式的详细信息，请参阅 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。 有关设置登录名和密码的代理的信息，请参阅 [管理登录名和密码在复制中的](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)。  
  
-   管理角色  
  
     确保使用正确的服务器和数据库角色进行复制的建立、维护和处理。 有关详细信息，请参阅 [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md)。  
  
-   发布访问列表 (PAL)  
  
     通过 PAL 授予对发布的访问权限。 PAL 的功能与 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 的访问控制列表相似。 当有订阅服务器连接到发布服务器或分发服务器并请求访问发布时，将对照 PAL 检查代理传递的身份验证信息。 有关详细信息和有关 PAL 的最佳做法，请参阅 [安全发布服务器](../../../relational-databases/replication/security/secure-the-publisher.md)。  
  
## 筛选已发布数据  
 除了使用身份验证和授权来控制对被复制的数据和对象的访问之外，复制还包含两个选项，用来控制订阅服务器上哪些数据可用：列筛选和行筛选。 有关筛选的详细信息，请参阅 [筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
 定义项目时，可以只发布那些发布所必需的列，而省略那些不必要或包含敏感数据的行。 例如，从 Adventure Works 数据库向现场销售代表发布 **Customer** 表时，可以省略 **AnnualSales** 列，该列可能仅与公司的高层管理者有关。  
  
 通过筛选已发布数据，可以限制对数据的访问，并可指定订阅服务器上的可用数据。 例如，可以筛选 **Customer** 表，以使公司合作伙伴们只收到其 **ShareInfo** 列的值为“yes”的客户的信息。 对于合并复制，如果使用包括 HOST_NAME() 的参数化筛选器，则需要考虑安全问题。 有关详细信息，请参阅"筛选使用 host_name （）"一节 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
## 另请参阅  
 [安全和保护与 #40;复制和 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [安全概述 & #40;复制和 #41;](../../../relational-databases/replication/security/security-overview-replication.md)   
 [威胁和漏洞缓解 & #40;复制和 #41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)  
  
  