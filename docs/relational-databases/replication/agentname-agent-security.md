---
title: "&lt;代理名称&gt; 代理安全性 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.agentnameagentsecurity.f1"
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# &lt;代理名称&gt; 代理安全性
   **\< 代理名称> 代理安全性** 页面允许您指定的帐户在其下的分发代理 （对于事务复制和快照复制） 或合并代理 （对于合并复制） 运行和复制拓扑中建立与计算机的连接。 所需权限的代理和复制安全性的最佳做法的信息，请参阅 [复制代理安全模式](../../relational-databases/replication/security/replication-agent-security-model.md) 和 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
## 选项  
 单击属性按钮 (**...**) 来访问每个订阅服务器的行中 **分发代理安全性** 或 **合并代理安全性** 对话框。 对于代理使用的帐户，有关其所需权限的详细信息，请在启动的对话框中单击 **“帮助”** 。  
  
 在一个对话框中输入设置后，将在网格中显示订阅服务器的连接信息。  
  
 **订阅服务器代理**  
 每个订阅服务器的名称。  
  
 **与分发服务器的连接**  
 为事务复制和快照复制显示。 连接到分发服务器时所处的上下文。 本地连接始终使用运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的上下文进行建立：  
  
-   对于推送订阅，本地连接是与分发服务器连接，因此此字段将始终显示︰ **模拟 '\< 域>\\< 登录名\>** 或 **模拟' \< 计算机>\\< 登录名\>** 对于推送订阅。  
  
-   对于请求订阅，还可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的上下文建立连接。 该字段显示以下项之一︰ **使用登录名 '\< 登录名>**, ，**模拟' \< 域>\\< 登录名\>** 或 **Impersonate \< 计算机>\\< 登录名\>**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用 Windows 帐户的上下文建立所有连接。  
  
 **与发布服务器和分发服务器的连接**  
 为合并复制显示。 与发布服务器和分发服务器建立连接时所处的上下文。 始终使用运行代理的 Windows 帐户的上下文建立本地连接：  
  
-   对于推送订阅，本地连接为与发布服务器和分发服务器上，连接，因此此字段将始终显示︰ **模拟 '\< 域>\\< 登录名\>** 或 **模拟' \< 计算机>\\< 登录名\>** 对于推送订阅。  
  
-   对于请求订阅，还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的上下文建立连接。 该字段显示以下项之一︰ **使用登录名 '\< 登录名>**, ，**模拟' \< 域>\\< 登录名\>** 或 **Impersonate \< 计算机>\\< 登录名\>**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用 Windows 帐户的上下文建立所有连接。  
  
 **与订阅服务器的连接**  
 与订阅服务器建立连接时所处的上下文。 始终使用运行代理的 Windows 帐户的上下文建立本地连接：  
  
-   对于请求订阅，本地连接为与订阅服务器连接，因此此字段将始终显示︰ **模拟 '\< 域>\\< 登录名\>** 或 **模拟' \< 计算机>\\< 登录名\>** 对于推送订阅。  
  
-   对于推送订阅，还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的上下文建立连接。 该字段显示以下项之一︰ **使用登录名 '\< 登录名>**, ，**模拟' \< 域>\\< 登录名\>** 或 **Impersonate \< 计算机>\\< 登录名\>**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用 Windows 帐户的上下文建立所有连接。  
  
## 另请参阅  
 [查看和修改请求订阅属性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [管理复制中的登录名和密码](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [复制代理安全性模式](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [安全和保护与 #40;复制和 #41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  