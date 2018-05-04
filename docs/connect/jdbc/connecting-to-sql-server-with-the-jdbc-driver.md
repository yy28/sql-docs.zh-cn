---
title: 连接到 SQL Server 使用 JDBC 驱动程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 526b0cbcd0a27adb7f2e8e848bf64a4f39198b54
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>通过 JDBC 驱动程序连接到 SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  你将使用执行操作的最基本项目之一[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]是连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 与数据库的所有交互都是通过[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)对象，而由于 JDBC 驱动程序具有此类的平面的体系结构，几乎所有有趣的行为与相接 SQLServerConnection 对象。  
  
 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]是仅在侦听 IPv6 端口设置 java.net.preferIPv6Addresses 系统属性，以确保，使用 IPv6 而非 IPv4 连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
```  
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 本部分中的主题介绍如何创建并连接到处理[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[创建连接 URL](../../connect/jdbc/building-the-connection-url.md)|介绍如何连接到窗体连接 URL[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 此外介绍了连接到命名实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。|  
|[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)|介绍各种连接属性和它们可以时如何使用连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。|  
|[设置数据源属性](../../connect/jdbc/setting-the-data-source-properties.md)|介绍如何在 Java Platform, Enterprise Edition 5 (Java EE) 环境中使用数据源。|  
|[使用连接](../../connect/jdbc/working-with-a-connection.md)|描述要在其中创建连接到的实例的各种方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。|  
|[使用连接池](../../connect/jdbc/using-connection-pooling.md)|说明 JDBC 驱动程序如何支持使用连接池。|  
|[使用数据库镜像&#40;JDBC&#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|说明 JDBC 驱动程序如何支持使用数据库镜像。|  
|[JDBC 驱动程序对高可用性和灾难恢复的支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|说明如何开发将连接到 AlwaysOn 可用性组的应用程序。|  
|[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|讨论应用程序连接到的 Java 实现[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库使用 Kerberos 集成身份验证。|  
|[连接到 Azure SQL 数据库](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|讨论 SQL Azure 数据库的连接问题。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
