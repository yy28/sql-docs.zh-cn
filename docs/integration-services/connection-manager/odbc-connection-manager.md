---
title: "ODBC 连接管理器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "连接 [Integration Services], ODBC"
  - "ODBC 连接管理器"
  - "数据源 [Integration Services], 连接"
  - "连接管理器 [Integration Services], ODBC"
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# ODBC 连接管理器
  ODBC 连接管理器使得包能够使用开放式数据库连接规范 (ODBC) 连接到多种数据库管理系统。  
  
 将 ODBC 连接添加到包并设置连接管理器的属性时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将创建连接管理器并将该连接管理器添加到包的 **Connections** 集合中。 该连接管理器在运行时决定物理 ODBC 连接。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **ODBC**。  
  
 可以用下列方式配置 ODBC 连接管理器：  
  
-   提供引用用户名或系统数据源名称的连接字符串。  
  
-   指定要连接的服务器。  
  
-   指示在运行时是否保留连接。  
  
## 配置 ODBC 连接管理器  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题之一：  
  
-   [ODBC 连接管理器用户界面参考](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和[以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## 另请参阅  
 [Integration Services (SSIS) 连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  