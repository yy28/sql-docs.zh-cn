---
title: 连接性疑难解答 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc0b307790452c1eeb347b4482a13c3f57ec05a6
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784868"
---
# <a name="troubleshooting-connectivity"></a>连接性疑难解答
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求安装并运行 TCP/IP 以与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库进行通信。 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器验证已安装了哪些网络库协议。  
  
 数据库连接失败的原因有多种。 包括下列原因：  
  
-   无法为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启用 TCP/IP，或者指定的服务器或端口号不正确。 验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否正通过指定服务器和端口上的 TCP/IP 进行侦听。 系统可能会报告类似“登录已经失败。 对主机的 TCP/IP 连接已失败。”的异常。 这指示下列内容之一：  
  
    -   已安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但并没有通过以下方法针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 TCP/IP 作为网络协议进行安装：使用 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 网络实用工具，或者使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
    -   已作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 协议安装了 TCP/IP，但是它并没有在 JDBC 连接 URL 中指定的端口上进行侦听。 默认端口为 1433，但是可以在安装产品时将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为在任意端口上进行侦听。 确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在端口 1433 上进行侦听。 或者，如果端口已更改，则应确保 JDBC 连接 URL 中指定的端口与更改的端口相匹配。 有关 JDBC 连接 Url 的详细信息，请参阅[创建连接 URL](../../connect/jdbc/building-the-connection-url.md)。  
  
    -   JDBC 连接 URL 中指定的计算机地址没有引用在其中安装并启动了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的服务器。  
  
    -   无法执行客户端和运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的服务器之间的 TCP/IP 的网络操作。 可以使用 telnet 检查 TCP/IP 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接性。 例如，在命令提示符中，键入 `telnet 192.168.0.0 1433`，此处 192.168.0.0 是正在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机地址，1433 是正在上面进行侦听的端口。 如果收到“Telnet 无法连接”的消息，TCP/IP 则没有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接的端口上进行侦听。 使用 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 网络实用工具或 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器以确保将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为在端口 1433 上使用 TCP/IP。  
  
    -   未在防火墙中打开服务器使用的端口。 这包括服务器使用的端口或与该服务器的指定实例相关联的端口（可选）。  
  
-   指定的数据库名称不正确。 确保所登录的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库是现有的数据库。  
  
-   用户名或密码不正确。 确保提供正确的值。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，JDBC 驱动程序要求安装带有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（默认为不启用）。 在安装或配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例时，应确保将此选项包含在内。  
  
## <a name="see-also"></a>另请参阅  
 [诊断与 JDBC 驱动程序有关的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
