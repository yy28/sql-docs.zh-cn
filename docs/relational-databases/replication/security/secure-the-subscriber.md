---
title: "保护订阅服务器的安全 | Microsoft Docs"
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
  - "订阅 [SQL Server 复制], 安全性"
  - "订阅方 [SQL Server 复制], 安全性"
  - "安全性 [SQL Server 复制], 订阅方"
ms.assetid: c8f0d62a-8b5d-4a21-9aec-223da52bb708
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 保护订阅服务器的安全
  合并代理和分发代理连接到订阅服务器。 这些连接可在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录或 Windows 登录上下文环境中建立。 在遵循授予必要的最小权限并且保护所有密码的存储的原则下，为这些代理提供合适的登录名十分重要。 有关每个代理所需权限的信息，请参阅 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## 分发代理  
 可以是每个订阅一个分发代理（独立代理，对于新建发布向导中创建的发布是默认设置），也可以是每个发布数据库和订阅数据库对一个分发代理（共享代理）。 T  
  
 若要指定对于推送订阅的连接信息，请参阅 [创建推送订阅](../../../relational-databases/replication/create-a-push-subscription.md)。  
  
 若要指定请求订阅的连接信息，请参阅 [创建请求订阅](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
## 合并代理  
 每个合并订阅都有自己的合并代理，此合并代理同时连接发布服务器和订阅服务器并对它们进行更新。  
  
 若要指定对于推送订阅的连接信息，请参阅 [创建推送订阅](../../../relational-databases/replication/create-a-push-subscription.md)。  
  
 若要指定请求订阅的连接信息，请参阅 [创建请求订阅](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## 立即更新订阅  
 当配置立即更新订阅时，需要在与发布服务器建立连接的订阅服务器上指定一个帐户。 连接用于在订阅服务器上激发的触发器，这些触发器用于将更改传播到发布服务器。 有三种连接类型可以选择：  
  
-   复制创建的链接服务器；此连接是用配置时所指定的凭据建立的。  
  
-   复制创建的链接服务器；用在订阅服务器上做更改的用户的凭据建立连接。  
  
-   已定义的链接服务器或远程服务器。  
  
> [!IMPORTANT]  
>  若要指定连接信息，请使用存储的过程 [sp_link_publication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)。 您还可以使用 **可更新订阅的登录名** 调用新建订阅向导页 **sp_link_publication**。 在某些情况下，如果订阅服务器运行的是 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Service Pack 1 (SP1) 或更高版本，而发布服务器运行的是早期版本，则该存储过程可能会失败。 如果在这种情形下存储过程失败，请将发布服务器升级到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SP1 或更高版本。  
  
 有关详细信息，请参阅 [创建事务发布的可更新订阅](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) 和 [查看和修改复制安全设置](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
> [!IMPORTANT]  
>  对于指定的连接帐户，只能授予对复制功能在发布数据库中创建的视图插入、更新和删除数据的权限，而不应授予任何其他权限。 授予权限的发布数据库中的视图的窗体中名为 **syncobj_***\< 十六进制>* 到每个订阅服务器上配置的帐户。  
  
## 排队更新订阅  
 当配置排队更新订阅时，请谨记以下两个与安全性相关的方面：  
  
-   每个分发服务器只有一个队列读取器代理。 建议最多为每个分发服务器配置一个为排队更新订阅而启用的发布。  
  
-   队列读取器代理建立与分发服务器、发布服务器和每个订阅服务器的连接：  
  
    -   运行代理并与分发服务器建立连接的账户将在创建代理时指定（如果使用新建发布向导，则代理将在创建为更新订阅而启用的发布时创建）。  
  
    -   代理与发布服务器建立连接的帐户将在配置发布服务器的分发时指定。 指定运行代理的 Windows 帐户，或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帐户。  
  
    -   代理与订阅服务器建立连接的帐户将在创建订阅时指定。  
  
    > [!IMPORTANT]  
    >  使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证连接到订阅服务器，并指定一个不同帐户连接到每个订阅服务器。 如果使用请求订阅，复制始终将连接设置为使用 Windows 身份验证（对于请求订阅，复制无法访问需要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证的订阅服务器上的元数据）。 这种情况下，请在配置订阅后对连接进行更改，以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证。  
  
     有关详细信息，请参阅如何︰ 创建事务发布 (SQL Server Management Studio) 的更新订阅和 [查看和修改复制安全设置](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
## 另请参阅  
 [启用加密的连接到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [复制安全最佳实践](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全和保护与 #40;复制和 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  