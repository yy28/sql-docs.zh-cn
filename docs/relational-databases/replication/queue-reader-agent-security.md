---
title: "队列读取器代理安全性 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.security.QRA.f1
helpviewer_keywords: Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e48ff4c40fb36b17818496300a3df1dbee511c22
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="queue-reader-agent-security"></a>队列读取器代理安全性
  可以使用 **“队列读取器代理安全性”** 对话框，指定用于运行队列读取器代理以及与分发服务器建立本地连接的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 代理使用 **“发布服务器属性”** 对话框（可通过 **“分发服务器属性”** 对话框访问）中指定的帐户连接发布服务器；代理使用与订阅的分发代理相同的上下文连接订阅服务器。 有关详细信息，请参阅 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 帐户必须有效，并为帐户指定正确的密码。 在运行代理之前不会对帐户和密码进行验证。  
  
## <a name="options"></a>选项  
 **进程帐户**  
 输入在分发服务器上运行队列读取器代理所用的 Windows 帐户。 指定的 Windows 帐户必须至少为分发数据库中的 **db_owner** 固定数据库角色的成员。  
  
 **“密码”** 和 **“确认密码”**  
 输入 Windows 帐户的密码。  
  
## <a name="see-also"></a>另请参阅  
 [管理复制中的登录名和密码](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [复制代理安全模式](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [复制代理概述](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
