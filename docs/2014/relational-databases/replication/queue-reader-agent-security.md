---
title: 队列读取器代理安全性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 657116e00b6905964f8cc65c28dff383c3cc9ad0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63261685"
---
# <a name="queue-reader-agent-security"></a>队列读取器代理安全性
  可以使用 **“队列读取器代理安全性”** 对话框，指定用于运行队列读取器代理以及与分发服务器建立本地连接的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 代理使用 **“发布服务器属性”** 对话框（可通过 **“分发服务器属性”** 对话框访问）中指定的帐户连接发布服务器；代理使用与订阅的分发代理相同的上下文连接订阅服务器。 有关详细信息，请参阅 [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md)。  
  
 帐户必须有效，并为帐户指定正确的密码。 在运行代理之前不会对帐户和密码进行验证。  
  
## <a name="options"></a>选项  
 **进程帐户**  
 输入在分发服务器上运行队列读取器代理所用的 Windows 帐户。 指定的 Windows 帐户必须至少为分发数据库中的 **db_owner** 固定数据库角色的成员。  
  
 **“密码”** 和 **“确认密码”**  
 输入 Windows 帐户的密码。  
  
## <a name="see-also"></a>另请参阅  
 [管理复制中的登录名和密码](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [复制代理安全模式](security/replication-agent-security-model.md)   
 [复制代理概述](agents/replication-agents-overview.md)   
 [复制安全最佳做法](security/replication-security-best-practices.md)  
  
  
