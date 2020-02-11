---
title: HTTP 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f79a882e3a3e4520cb8cfcd4468f3c908b79abf5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833743"
---
# <a name="http-connection-manager"></a>HTTP 连接管理器
  利用 HTTP 连接，包可以使用 HTTP 访问 Web 服务器以发送或接收文件。 包含的 Web 服务任务[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用此连接管理器。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
 将 HTTP 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 HTTP 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包的 `Connections` 集合。  
  
 连接`ConnectionManagerType`管理器的属性设置为`HTTP.`  
  
 可以通过下列方式配置 HTTP 连接管理器：  
  
-   使用凭据。 如果连接管理器使用凭据，则其属性包含用户名、密码和域。  
  
    > [!IMPORTANT]  
    >  HTTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
-   使用客户端证书。 如果连接管理器使用客户端证书，则其属性包含证书名称。  
  
-   提供连接到服务器的超时值和写入数据的块区大小。  
  
-   使用代理服务器。 也可以将代理服务器配置为使用凭据，并跳过代理服务器而使用本地地址。  
  
## <a name="configuration-of-the-http-connection-manager"></a>HTTP 连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [HTTP 连接管理器编辑器 &#40;服务器页面&#41;](../http-connection-manager-editor-server-page.md)  
  
-   [HTTP 连接管理器编辑器 &#40;代理页面&#41;](../http-connection-manager-editor-proxy-page.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>。  
  
## <a name="see-also"></a>另请参阅  
 [Web 服务任务](../control-flow/web-service-task.md)   
 [Integration Services (SSIS) 连接](integration-services-ssis-connections.md)  
  
  
