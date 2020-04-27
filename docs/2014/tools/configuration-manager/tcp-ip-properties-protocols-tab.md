---
title: TCP-IP 属性（"协议" 选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b545fbe28e28739b5f66a7beca1ab7c0450ae08a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150460"
---
# <a name="tcp---ip-properties-protocols-tab"></a>TCP-IP 属性（"协议" 选项卡）
  使用“TCP/IP 属性”  对话框可以配置 TCP/IP 协议的选项。 在左窗格中单击 **TCP/IP** 以在详细信息窗格中显示单个 IP 地址配置。  
  
 必须重新启动 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，更改才会生效。  
  
## <a name="options"></a>选项  
 **已启用**  
 可能的值为“是”  和“否”  。  
  
 **Keep Alive**  
 指定传输保持活动状态的数据包的时间间隔（毫秒），以检查位于连接远端的计算机是否仍可用。  
  
 **Listen All**  
 指定 SQL Server 是否侦听所有绑定到计算机网卡的 IP 地址。 如果设置为“否”  ，则使用每个 IP 地址的各自属性对话框分别对每个 IP 地址进行配置。 如果设置为“是”  ，则 **IPAll** 属性框的设置将应用到所有的 IP 地址。 默认值为“是”  。  
  
 **No Delay**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会实施对此属性的更改。  
  
## <a name="see-also"></a>另请参阅  
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [使用 TCP IP 创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
  
