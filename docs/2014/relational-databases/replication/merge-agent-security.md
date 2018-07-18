---
title: 合并代理安全性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.MA.f1
helpviewer_keywords:
- Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8593023d1ff8ed332bbd3480a56f8c15b366e23
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191677"
---
# <a name="merge-agent-security"></a>合并代理安全性
  可以使用 **“合并代理安全性”** 对话框指定用于运行合并代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 对于推送订阅，合并代理在分发服务器上运行；对于请求订阅，合并代理在订阅服务器上运行。 Windows 帐户也称为“进程帐户 ”，因为代理进程是在此帐户下运行。 该对话框中可用的其他选项取决于访问对话框的方式：  
  
-   如果从新建订阅向导访问该对话框，您还可以指定合并代理在建立与订阅服务器（对于推送订阅）或发布服务器和分发服务器（对于请求订阅）的连接时所使用的上下文。 可以使用 Windows 帐户或指定的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户的上下文来建立连接。  
  
-   如果从 **“订阅属性”** 对话框访问该对话框，可通过单击该对话框的 **“订阅服务器连接”** 或 **“发布服务器连接”** 行中的属性按钮 ( **...** ) 来指定合并代理建立连接时所使用的上下文。 有关访问“订阅属性”对话框的详细信息，请参阅[查看和修改推送订阅属性](view-and-modify-push-subscription-properties.md)和如何[查看和修改请求订阅属性](view-and-modify-pull-subscription-properties.md)。  
  
 所有帐户必须是有效的，并且为每个帐户指定了正确的密码。 在运行代理之前不会对帐户和密码进行验证。  
  
## <a name="options"></a>“常规”  
 **进程帐户**  
 输入运行合并代理所使用的 Windows 帐户。  
  
-   对于推送订阅，该帐户必须：  
  
    -   至少是分发数据库中的 **db_owner** 固定数据库角色的成员。  
  
    -   是 PAL 的成员。  
  
    -   是与发布数据库中的某个用户关联的登录名。  
  
    -   对快照共享拥有读取权限。  
  
-   对于请求订阅，该帐户必须至少为订阅数据库中的 **db_owner** 固定数据库角色的成员。  
  
 如果在建立连接时模拟进程帐户，则还需要其他权限。 请参阅下面的 **“连接到发布服务器和分发服务器”** 和 **“连接到订阅服务器”** 部分。  
  
 由于合并代理没有运行在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 实例上，因此不能为对 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的请求订阅指定 **“进程帐户”**。  
  
 **“密码”** 和 **“确认密码”**  
 输入 Windows 帐户的密码。  
  
 **“连接到发布服务器和分发服务器”**  
 对于推送订阅，始终通过模拟在 **“进程帐户”** 文本框中指定的帐户来建立与发布服务器和分发服务器的连接。  
  
 对于请求订阅，请选择合并代理是通过模拟在 **“进程帐户”** 文本框中指定的帐户，还是通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户来建立与发布服务器和分发服务器的连接。 如果选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户，请输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和密码。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议您选择模拟 Windows 帐户，而不要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户。  
  
 连接所用的 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户必须：  
  
-   是 PAL 的成员。  
  
-   是与发布数据库中的某个用户关联的登录名。  
  
-   是与分发数据库中的用户关联的登录名（用户可以是 Guest 用户）。  
  
-   对快照共享拥有读取权限。  
  
 **“连接到订阅服务器”**  
 对于请求订阅，始终通过模拟 **“进程帐户”** 文本框中指定的帐户来建立与订阅服务器的连接。  
  
 对于推送订阅，请选择合并代理是通过模拟在 **“进程帐户”** 文本框中指定的帐户，还是通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户来建立与发布服务器和分发服务器的连接。 如果选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户，请输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和密码。  
  
> [!NOTE]  
>  建议您选择模拟 Windows 帐户，而不要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户。  
  
 连接订阅服务器所用的 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户必须至少为订阅数据库中的 **db_owner** 固定数据库角色的成员。  
  
## <a name="see-also"></a>请参阅  
 [管理复制中的登录名和密码](security/manage-logins-and-passwords-in-replication.md)   
 [复制代理安全模式](security/replication-agent-security-model.md)   
 [复制代理概述](agents/replication-agents-overview.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
