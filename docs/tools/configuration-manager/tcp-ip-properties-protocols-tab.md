---
title: "TCP/IP 属性（“协议”选项卡） | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "TCP/IP [SQL Server], 配置选项"
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# TCP/IP 属性（“协议”选项卡）
  使用“TCP/IP 属性”对话框可以配置 TCP/IP 协议的选项。 在左窗格中单击 **TCP/IP** 以在详细信息窗格中显示单个 IP 地址配置。  
  
 必须重新启动 Microsoft SQL Server，更改才会生效。  
  
## 选项  
 **Enabled**  
 可能的值为“是”和“否”。  
  
 **Keep Alive**  
 指定传输保持活动状态的数据包的时间间隔（毫秒），以检查位于连接远端的计算机是否仍可用。  
  
 **Listen All**  
 指定 SQL Server 是否侦听所有绑定到计算机网卡的 IP 地址。 如果设置为“否”，则使用每个 IP 地址的各自属性对话框分别对每个 IP 地址进行配置。 如果设置为“是”，则 **IPAll** 属性框的设置将应用到所有的 IP 地址。 默认值为“是”。  
  
 **No Delay**  
 SQL Server 不会实施对此属性的更改。  
  
## 另请参阅  
 [选择网络协议](https://msdn.microsoft.com/library/ms187892(v=sql.130).aspx)   
 [使用 TCP IP 创建有效的连接字符串](https://msdn.microsoft.com/library/ms191260.aspx)  
  
  