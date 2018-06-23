---
title: SQL Native Client 11.0 配置 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- client configuration [SQL Server], SQL Server Native Client
ms.assetid: e73143e9-5e7b-4d0a-8827-ab900efdcb35
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f83aa59c76750a0e6384a88e9755b0c51333bb58
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025365"
---
# <a name="sql-native-client-110-configuration"></a>SQL Native Client 11.0 配置
  本节包含了按 F1 后看到的有关  配置管理器中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对话框的帮助主题。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 是客户端计算机用于连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的网络库，与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起启动。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 配置中配置的设置将在运行客户端程序的计算机上使用。 在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的计算机上配置这些设置时，它们仅影响那些运行在服务器上的客户端程序。  
  
 这些设置不会影响连接到早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的客户端，除非它们使用与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起启动的客户端工具，例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [SQL Server Native Client 配置属性&#40;标志选项卡&#41;](../../../2014/tools/configuration-manager/sql-server-native-client-configuration-properties-flags-tab.md)  
  
-   [客户端协议&#40;SQL Server 配置管理器&#41;](../../relational-databases/sql-server-configuration-manager.md)  
  
    -   [客户端协议属性&#40;排序选项卡&#41;](../../../2014/tools/configuration-manager/client-protocols-properties-order-tab.md)  
  
    -   [客户端协议-Shared Memory 属性&#40;协议选项卡&#41;](../../../2014/tools/configuration-manager/client-protocols-shared-memory-properties-protocol-tab.md)  
  
    -   [客户端协议-TCP 和 IP 属性&#40;协议选项卡&#41;](../../../2014/tools/configuration-manager/client-protocols-tcp-and-ip-properties-protocol-tab.md)  
  
    -   [客户端协议-Named Pipes 属性&#40;协议选项卡&#41;](../../../2014/tools/configuration-manager/client-protocols-named-pipes-properties-protocol-tab.md)  
  
-   [别名&#40;SQL Server 配置管理器&#41;](../../../2014/tools/configuration-manager/aliases-sql-server-configuration-manager.md)  
  
    -   [新别名&#40;别名选项卡&#41;](../../../2014/tools/configuration-manager/new-alias-alias-tab.md)  
  
    -   [&#60;别名&#62;属性&#40;别名选项卡&#41;](../../../2014/tools/configuration-manager/alias-properties-alias-tab.md)  
  
    -   [使用 Shared Memory 协议创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
    -   [使用 TCP IP 创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
    -   [使用命名管道创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)  
  
  