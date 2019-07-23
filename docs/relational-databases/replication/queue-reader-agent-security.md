---
title: 队列读取器代理安全性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 92b80f727ce87606b0c1c58954b0743734880422
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021266"
---
# <a name="queue-reader-agent-security"></a>队列读取器代理安全性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以使用 **“队列读取器代理安全性”** 对话框，指定用于运行队列读取器代理以及与分发服务器建立本地连接的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 代理使用 **“发布服务器属性”** 对话框（可通过 **“分发服务器属性”** 对话框访问）中指定的帐户连接发布服务器；代理使用与订阅的分发代理相同的上下文连接订阅服务器。 有关详细信息，请参阅 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 帐户必须有效，并为帐户指定正确的密码。 在运行代理之前不会对帐户和密码进行验证。  
  
## <a name="options"></a>选项  
 **进程帐户**  
 输入在分发服务器上运行队列读取器代理所用的 Windows 帐户。 指定的 Windows 帐户必须至少为分发数据库中的 **db_owner** 固定数据库角色的成员。  
  
 **“密码”** 和 **“确认密码”**  
 输入 Windows 帐户的密码。  
  
## <a name="see-also"></a>另请参阅  
 [复制的标识和访问控制](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [复制代理安全模式](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [复制代理概述](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [复制安全最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
