---
title: TCP/IP 属性 （协议选项卡） |Microsoft 文档
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f7731e5ee583c4b1356c9a538ee41a3a475c613
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="tcpip-properties-protocols-tab"></a>TCP/IP 属性（“协议”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  使用“TCP/IP 属性”对话框可以配置 TCP/IP 协议的选项。 在左窗格中单击 **TCP/IP** 以在详细信息窗格中显示单个 IP 地址配置。  
  
 必须重新启动 Microsoft SQL Server，更改才会生效。  
  
## <a name="options"></a>“常规”  
 **已启用**  
 可能的值为“是”和“否”。  
  
 **Keep Alive**  
 指定传输保持活动状态的数据包的时间间隔（毫秒），以检查位于连接远端的计算机是否仍可用。  
  
 **Listen All**  
 指定 SQL Server 是否侦听所有绑定到计算机网卡的 IP 地址。 如果设置为“否”，则使用每个 IP 地址的各自属性对话框分别对每个 IP 地址进行配置。 如果设置为“是”，则 **IPAll** 属性框的设置将应用到所有的 IP 地址。 默认值为“是”。  
  
 **No Delay**  
 SQL Server 不会实施对此属性的更改。  
  
## <a name="see-also"></a>另请参阅  
 [选择网络协议](https://msdn.microsoft.com/library/ms187892(v=sql.130).aspx)   
 [使用 TCP IP 创建有效的连接字符串](creating-a-valid-connection-string-using-tcp-ip.md)  
  
  
