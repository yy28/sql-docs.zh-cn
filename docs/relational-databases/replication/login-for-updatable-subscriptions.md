---
title: "可更新订阅的登录名 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.updatablesubscriptionslogin.f1"
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# 可更新订阅的登录名
  对于立即更新，如果您选择 **复制** 上 **可更新订阅** 页上的此向导中，您必须与订阅服务器在建立到发布服务器的连接中指定的帐户。 
  
 连接使用的触发器的激发在订阅服务器上，并将更改传播到发布服务器。 此帐户是必需的即使您选择 **更改进行排队并在可能时提交** 上 **可更新订阅** 页。 默认情况下在新建订阅向导将排队更新切换到立即更新，如果所需的功能的配置。  
  
> **重要说明!!** 为连接只应指定该帐户授予权限以插入、 更新和删除复制的数据在视图上创建的发布数据库中。 它不应该再授予任何其他权限。 授予对视图中名为窗体中的发布数据库的权限 **syncobj_***\< 十六进制>* 到每个订阅服务器上配置的帐户。  
  
 有三种连接类型可以选择：  
  
-   已定义的链接服务器或远程服务器。  
  
-   复制创建的链接服务器；用在此向导中指定的凭据建立连接。  
  
-   复制创建的链接服务器；用在订阅服务器上做更改的用户的凭据建立连接。  
  
 可以在此向导中指定前两个选项。 最后一个选项只能指定使用 [sp_link_publication &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md);将值指定为 **1** 参数 **@security_mode**。  
  
## 选项  
 **创建使用以下 SQL Server 身份验证登录名进行连接的链接服务器：**  
 复制创建链接的服务器使用的凭据中指定 **登录** 和 **密码** 字段。  
  
 **登录**  
 输入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有仅在本主题中所述的权限的登录名。  
  
 **密码**  
 在指定的登录名输入一个强密码 **登录**。  
    
 **使用您指定的链接服务器或远程服务器。**  
 此选项需要使用您所定义的链接服务器或远程服务器。 有关详细信息，请参阅 [链接服务器 &#40; 数据库引擎 &#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) 和 [远程服务器](../../database-engine/configure-windows/remote-servers.md)。 请确保用于链接服务器或远程服务器的登录名具有强密码，并且仅具有本主题中描述的权限。  
  
## 另请参阅  
 [创建事务发布的可更新订阅](https://msdn.microsoft.com/library/ms152769.aspx)   
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [事务复制的可更新订阅](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  