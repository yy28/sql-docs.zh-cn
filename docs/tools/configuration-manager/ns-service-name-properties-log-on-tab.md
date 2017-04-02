---
title: "NS$&lt;服务器名称&gt; 属性（“登录”选项卡） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5e6816ec-d4c5-4429-8033-b97427584890
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# NS$&lt;服务器名称&gt; 属性（“登录”选项卡）
  使用 **“Notification Services 属性”** 对话框中的 **“登录”** 选项卡可以指定 [!INCLUDE[ssNS](../../includes/ssns-md.md)] 服务使用的帐户，还可以启动和停止该服务。  
  
## 选项  
 **本地系统帐户**  
 指定一个不要求输入密码的本地系统帐户。 不过，本地系统帐户可能会限制该服务与其他服务器进行交互，具体取决于该帐户所拥有的权限。  
  
 **本帐户**  
 指定一个使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证的本地用户帐户或域用户帐户。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用具有最低服务权限的域用户帐户。 有关选择帐户的详细信息，请在联机丛书中搜索主题“设置 Windows 服务帐户”。  
  
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
  
  