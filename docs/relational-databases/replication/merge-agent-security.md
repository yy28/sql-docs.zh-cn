---
title: "合并代理安全性 | Microsoft Docs"
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
  - "sql13.rep.security.MA.f1"
helpviewer_keywords: 
  - "“合并代理安全性”对话框"
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 合并代理安全性
  可以使用 **“合并代理安全性”** 对话框指定用于运行合并代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 对于推送订阅，合并代理在分发服务器上运行；对于请求订阅，合并代理在订阅服务器上运行。 Windows 帐户也称为“进程帐户 ”，因为代理进程是在此帐户下运行。 该对话框中可用的其他选项取决于访问对话框的方式：  
  
-   如果从新建订阅向导访问该对话框，您还可以指定合并代理在建立与订阅服务器（对于推送订阅）或发布服务器和分发服务器（对于请求订阅）的连接时所使用的上下文。 可以使用 Windows 帐户或指定的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户的上下文来建立连接。  
  
-   如果对话框中访问从 **订阅属性** 对话框框中，指定在其下合并代理在通过单击属性按钮建立连接的上下文 (**...**) 中 **订阅服务器连接** 或 **发布服务器连接** 该对话框中的一行。 有关访问 **订阅属性** 对话框中，请参阅 [查看和修改推送订阅属性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 和操作方法︰ [查看和修改请求订阅属性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
 所有帐户必须是有效的，并且为每个帐户指定了正确的密码。 在运行代理之前不会对帐户和密码进行验证。  
  
## 选项  
 **进程帐户**  
 输入运行合并代理所使用的 Windows 帐户。  
  
-   对于推送订阅，该帐户必须：  
  
    -   至少是属于 **db_owner** 分发数据库中的固定的数据库角色。  
  
    -   是 PAL 的成员。  
  
    -   是与发布数据库中的某个用户关联的登录名。  
  
    -   对快照共享拥有读取权限。  
  
-   对于请求订阅，该帐户必须至少是成员的 **db_owner** 订阅数据库中的固定的数据库角色。  
  
 如果在建立连接时模拟进程帐户，则还需要其他权限。 请参阅下面的 **“连接到发布服务器和分发服务器”** 和 **“连接到订阅服务器”** 部分。  
  
 **进程帐户** 对请求订阅，不能指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], ，这是因为的实例上不运行合并代理 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。  
  
 **密码** 和 **确认密码**  
 输入 Windows 帐户的密码。  
  
 **连接到发布服务器和分发服务器**  
 对于推送订阅与发布服务器和分发服务器的连接始终通过模拟中指定的帐户建立 **进程帐户** 文本框。  
  
 对于请求订阅，请选择合并代理是通过模拟在 **“进程帐户”** 文本框中指定的帐户，还是通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户来建立与发布服务器和分发服务器的连接。 如果选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户，请输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和密码。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议您选择模拟 Windows 帐户，而不是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户。  
  
 连接所用的 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户必须：  
  
-   是 PAL 的成员。  
  
-   是与发布数据库中的某个用户关联的登录名。  
  
-   是与分发数据库中的用户关联的登录名（用户可以是 Guest 用户）。  
  
-   对快照共享拥有读取权限。  
  
 **连接到订阅服务器**  
 对于请求订阅，订阅服务器上的连接始终通过模拟中指定的帐户建立 **进程帐户** 文本框。  
  
 对于推送订阅，请选择合并代理是通过模拟在 **“进程帐户”** 文本框中指定的帐户，还是通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户来建立与发布服务器和分发服务器的连接。 如果选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户，请输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和密码。  
  
> [!NOTE]  
>  建议您选择模拟 Windows 帐户，而不要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户。  
  
 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于连接到订阅服务器上的帐户必须至少是属于 **db_owner** 订阅数据库中的固定的数据库角色。  
  
## 另请参阅  
 [管理复制中的登录名和密码](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [复制代理安全性模式](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [复制代理概述](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  