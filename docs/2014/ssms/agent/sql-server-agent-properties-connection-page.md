---
title: SQL Server 代理属性（“连接”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b633551c252b5edde1af3ad87b4d932d542a7bb
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43813433"
---
# <a name="sql-server-agent-properties-connection-page"></a>SQL Server 代理属性（“连接”页）
  使用此页可查看和修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之间的连接设置。  
  
## <a name="options"></a>选项  
 **本地主机服务器别名**  
 指定用来连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本地实例的别名。 如果无法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的默认连接选项，请为相应的实例定义一个别名，并在此处指定该别名。  
  
 **使用 Windows 身份验证**  
 将 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证设置为连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时使用的身份验证方法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理按运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务的帐户的身份进行连接。  
  
 **Use SQL Server Authentication**  
 将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证设置为连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时使用的身份验证方法。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供身份验证是为了向后兼容。 为了增强安全性，请使用 Windows 身份验证（如果可能的话）。  
  
 **登录**  
 指定用于连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的登录名。  
  
 **密码**  
 指定用于连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的密码。  
  
  
