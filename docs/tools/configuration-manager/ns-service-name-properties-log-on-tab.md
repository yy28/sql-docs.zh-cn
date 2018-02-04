---
title: "NS$&lt;服务名称&gt;属性 （日志选项卡上） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e6816ec-d4c5-4429-8033-b97427584890
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 512d1281ca516256631845d0283b50f8f58f82d5
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="nsltservice-namegt-properties-log-on-tab"></a>NS$&lt;服务名称&gt;属性 （日志选项卡上）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
使用 **“Notification Services 属性”** 对话框中的 **“登录”** 选项卡可以指定 [!INCLUDE[ssNS](../../includes/ssns-md.md)] 服务使用的帐户，还可以启动和停止该服务。  
  
## <a name="options"></a>选项  
 **本地系统帐户**  
 指定一个不要求输入密码的本地系统帐户。 不过，本地系统帐户可能会限制该服务与其他服务器进行交互，具体取决于该帐户所拥有的权限。  
  
 **本帐户**  
 指定一个使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证的本地用户帐户或域用户帐户。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]建议使用具有最低权限的域用户帐户，服务。 有关选择帐户的详细信息，请在联机丛书中搜索主题“设置 Windows 服务帐户”。  
  
 **帐户名**  
 指定本地用户帐户名或域用户帐户名。  
  
 **密码**  
 键入帐户的密码。  
  
 **确认密码**  
 再次键入帐户的密码。  
  
 **开始**  
 启动服务。  
  
 **停止**  
 停止服务。  
  
 **暂停**  
 暂停服务。  
  
 **恢复**  
 恢复暂停的服务。  
  
  
