---
title: "HTTP 连接管理器 | Microsoft Docs"
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
  - "HTTP 连接管理器"
  - "网站连接 [Integration Services]"
  - "连接管理器 [Integration Services], HTTP"
  - "Web 服务器连接 [Integration Services]"
  - "连接 [Integration Services], HTTP"
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# HTTP 连接管理器
  利用 HTTP 连接，包可以使用 HTTP 访问 Web 服务器以发送或接收文件。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 Web 服务任务使用此连接管理器。  
  
 将 HTTP 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 HTTP 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包的 **Connections** 集合。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **HTTP.**。  
  
 可以通过下列方式配置 HTTP 连接管理器：  
  
-   使用凭据。 如果连接管理器使用凭据，则其属性包含用户名、密码和域。  
  
    > [!IMPORTANT]  
    >  HTTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
-   使用客户端证书。 如果连接管理器使用客户端证书，则其属性包含证书名称。  
  
-   提供连接到服务器的超时值和写入数据的块区大小。  
  
-   使用代理服务器。 也可以将代理服务器配置为使用凭据，并跳过代理服务器而使用本地地址。  
  
## HTTP 连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [HTTP 连接管理器编辑器（“服务器”页）](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
-   [HTTP 连接管理器编辑器（“代理”页）](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>。  
  
## 另请参阅  
 [Web 服务任务](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services (SSIS) 连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  