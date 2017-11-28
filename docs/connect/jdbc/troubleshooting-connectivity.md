---
title: "故障排除连接 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1566b30797b45a0eaa40491658f4fc3381c683f9
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="troubleshooting-connectivity"></a>连接疑难解答
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求 TCP/IP 已安装并正在运行与通信你[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 你可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]配置管理器以验证安装了哪些网络库协议。  
  
 数据库连接失败的原因有多种。 包括下列原因：  
  
-   未启用 TCP/IP [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，或指定的服务器或端口号不正确。 验证[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]正在侦听 TCP/IP 与指定的服务器和端口。 系统可能会报告类似“登录已经失败。 对主机的 TCP/IP 连接已失败。”的异常。 这指示下列内容之一：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]已安装但尚未安装 TCP/IP 网络协议的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]网络实用程序[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Configuration Manager for[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]及更高版本。  
  
    -   作为安装 TCP/IP[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]协议，但它未在侦听 JDBC 连接 URL 中指定的端口。 默认端口为 1433，但[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可以配置在产品安装在任何端口上侦听。 请确保[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]侦听端口 1433年。 或者，如果端口已更改，则应确保 JDBC 连接 URL 中指定的端口与更改的端口相匹配。 有关 JDBC 连接 Url 的详细信息，请参阅[生成连接 URL](../../connect/jdbc/building-the-connection-url.md)。  
  
    -   JDBC 连接中指定的计算机的地址 URL 不是指服务器其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]安装并启动。  
  
    -   TCP/IP 的网络操作之间的客户端和服务器运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不是可操作。 你可以检查 TCP/IP 连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过 telnet。 例如，在命令提示符处，键入`telnet 192.168.0.0 1433`192.168.0.0 其中是正在运行的计算机的地址[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和 1433年是它正在侦听的端口。 如果你收到一条指出"无法连接 Telnet"消息，TCP/IP 未在侦听该端口[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]连接。 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]网络实用程序[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Configuration Manager for[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]和更高版本，确保[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]配置为在端口 1433年上使用 TCP/IP。  
  
    -   未在防火墙中打开服务器使用的端口。 这包括服务器使用的端口或与该服务器的指定实例相关联的端口（可选）。  
  
-   指定的数据库名称不正确。 请确保你登录到一个现有[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
-   用户名或密码不正确。 确保提供正确的值。  
  
-   当你使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，JDBC 驱动程序需要的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]随[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，这不是默认值。 请确保你安装或配置你的实例时，此选项将包括[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [诊断 JDBC 驱动程序的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
