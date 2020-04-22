---
title: 通过 JDBC 驱动程序连接到 SQL Server | Microsoft Docs
description: 使用 Microsoft JDBC Driver for SQL Server 连接到数据库时，与数据库的所有交互都通过 SQLServerConnection 对象进行。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1089960af020e648586f59914ccc91e99bf0b9af
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487961"
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>通过 JDBC 驱动程序连接到 SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  对 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 执行的最基本的操作之一是建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接。 与数据库的所有交互都通过 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 对象实现，并且由于 JDBC 驱动程序具有这种平面体系结构，因此几乎所有相关行为都涉及 SQLServerConnection 对象。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仅侦听 IPv6 端口，请设置 java.net.preferIPv6Addresses 系统属性，确保使用 IPv6 而不是 IPv4 来连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：  
  
```java
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 本部分中的主题说明如何建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接以及如何使用该连接。  
  
## <a name="in-this-section"></a>在本节中  
  
|主题|说明|  
|-----------|-----------------|  
|[生成连接 URL](../../connect/jdbc/building-the-connection-url.md)|说明如何构建连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接 URL。 并说明到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库指定实例的连接。|  
|[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)|说明各种连接属性以及如何在连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库时使用这些属性。|  
|[设置数据源属性](../../connect/jdbc/setting-the-data-source-properties.md)|介绍如何在 Java Platform, Enterprise Edition 5 (Java EE) 环境中使用数据源。|  
|[处理连接](../../connect/jdbc/working-with-a-connection.md)|说明创建与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接实例的各种方法。|  
|[使用连接池](../../connect/jdbc/using-connection-pooling.md)|说明 JDBC 驱动程序如何支持使用连接池。|  
|[使用数据库镜像 &#40;JDBC&#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|说明 JDBC 驱动程序如何支持使用数据库镜像。|  
|[JDBC 驱动程序对高可用性和灾难恢复的支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|说明如何开发将连接到 AlwaysOn 可用性组的应用程序。|  
|[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|讨论一个可供应用程序使用 Kerberos 集成身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的 Java 实现。|  
|[连接到 Azure SQL 数据库](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|讨论 SQL Azure 数据库的连接问题。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
