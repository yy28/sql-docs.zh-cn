---
title: 查找服务器（网络服务器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ffa52839c20a34574423e3b123da79f734fb69ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786681"
---
# <a name="browse-for-servers-network-servers"></a>查找服务器（网络服务器）
  如果要连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件但不知道 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的确切名称，请在“服务器名称”  框中单击“浏览更多”  ，以打开“查找服务器”  对话框。  
  
 将通过服务器计算机上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服务填充此对话框。 列表中未显示实例名称的原因有多种：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服务可能未在运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的计算机上运行。  
  
-   UDP 端口 1434 可能被防火墙阻塞。  
  
-   可能设置了 **HideInstance** 标志。  
  
 若要连接到列表中未列出的实例，请键入该实例的完整连接字符串，其中包括 TCP/IP 端口号或 Named Pipes 管道名称。  
  
## <a name="options"></a>选项  
 **在网络中选择要连接的 SQL Server 实例**  
 单击树中显示的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，指定要连接的服务器。 可以显示或隐藏部分树视图方法标记为在节点上，单击 **+** 或 **-** 符号。  
  
  
