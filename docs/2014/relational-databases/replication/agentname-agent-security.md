---
title: '&lt;代理名称&gt; 代理安全性 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d77f8d6acb449bc9aa2298dbcba9782fd7bc07e7
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127433"
---
# <a name="ltagentnamegt-agent-security"></a>&lt;代理名称&gt; 代理安全性
  使用“\<代理名称> 代理安全性”页，你可以指定用来运行分发代理（对于事务复制和快照复制）或合并代理（对于合并复制）的帐户，并与复制拓扑中的计算机建立连接。 有关代理要求的权限及复制安全的最佳实践的信息，请参阅[复制代理安全模型](security/replication-agent-security-model.md)和[复制安全性最佳做法](security/replication-security-best-practices.md)。  
  
## <a name="options"></a>选项  
 单击每个订阅服务器的行中的属性按钮 (**...**)，可以访问 **“分发代理安全性”** 或 **“合并代理安全性”** 对话框。 对于代理使用的帐户，有关其所需权限的详细信息，请在启动的对话框中单击 **“帮助”** 。  
  
 在一个对话框中输入设置后，将在网格中显示订阅服务器的连接信息。  
  
 **订阅服务器代理**  
 每个订阅服务器的名称。  
  
 **与分发服务器的连接**  
 为事务复制和快照复制显示。 连接到分发服务器时所处的上下文。 本地连接始终使用运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的上下文进行建立：  
  
-   对于推送订阅，本地连接是指与分发服务器的连接，因此此字段将始终显示：**Impersonate '\<域 >\\< 登录名\>'** 或**Impersonate\<计算机 >\\< 登录名\>** 推送订阅。  
  
-   对于请求订阅，还可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的上下文建立连接。 该字段显示下列选项之一：**使用登录名\<登录名 >'**， **Impersonate '\<域 >\\< 登录名\>'** 或**Impersonate\<计算机 >\\< 登录名\>**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用 Windows 帐户的上下文建立所有连接。  
  
 **与发布服务器和分发服务器的连接**  
 为合并复制显示。 与发布服务器和分发服务器建立连接时所处的上下文。 始终使用运行代理的 Windows 帐户的上下文建立本地连接：  
  
-   对于推送订阅，本地连接是指与发布服务器和分发服务器的连接，因此此字段将始终显示：**Impersonate '\<域 >\\< 登录名\>'** 或**Impersonate\<计算机 >\\< 登录名\>** 推送订阅。  
  
-   对于请求订阅，还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的上下文建立连接。 该字段显示下列选项之一：**使用登录名\<登录名 >'**， **Impersonate '\<域 >\\< 登录名\>'** 或**Impersonate\<计算机 >\\< 登录名\>**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用 Windows 帐户的上下文建立所有连接。  
  
 **与订阅服务器的连接**  
 与订阅服务器建立连接时所处的上下文。 始终使用运行代理的 Windows 帐户的上下文建立本地连接：  
  
-   对于请求订阅，本地连接是指与订阅服务器的连接，因此此字段将始终显示：**Impersonate '\<域 >\\< 登录名\>'** 或**Impersonate\<计算机 >\\< 登录名\>** 推送订阅。  
  
-   对于推送订阅，还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的上下文建立连接。 该字段显示下列选项之一：**使用登录名\<登录名 >'**， **Impersonate '\<域 >\\< 登录名\>'** 或**Impersonate\<计算机 >\\< 登录名\>**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用 Windows 帐户的上下文建立所有连接。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改请求订阅属性](view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](view-and-modify-push-subscription-properties.md)   
 [管理复制中的登录名和密码](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [复制代理安全模式](security/replication-agent-security-model.md)   
 [SQL Server 复制安全性](security/view-and-modify-replication-security-settings.md)  
  
  
