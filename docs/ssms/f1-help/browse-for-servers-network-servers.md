---
title: "查找服务器（网络服务器）| Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0dfaef0364cf72e994b0fe5de778adc8a18bd715
ms.lasthandoff: 04/11/2017

---
# <a name="browse-for-servers-network-servers"></a>查找服务器（网络服务器）
如果要连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 组件但不知道 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例的确切名称，请在“服务器名称”框中单击“浏览更多”，以打开“查找服务器”对话框。  
  
将通过服务器计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Browser 服务填充此对话框。 列表中未显示实例名称的原因有多种：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Browser 服务可能未在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的计算机上运行。  
  
-   UDP 端口 1434 可能被防火墙阻塞。  
  
-   可能设置了 **HideInstance** 标志。  
  
若要连接到列表中未列出的实例，请键入该实例的完整连接字符串，其中包括 TCP/IP 端口号或 Named Pipes 管道名称。  
  
## <a name="options"></a>选项  
**在网络中选择要连接的 SQL Server 实例**  
单击树中显示的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例，指定要连接的服务器。 单击带有 **+** 或 **–** 符号的节点可以显示或隐藏部分树视图。  
  

