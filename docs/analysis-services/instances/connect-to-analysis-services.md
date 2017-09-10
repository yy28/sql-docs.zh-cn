---
title: "连接到 Analysis Services |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- instances of Analysis Services, connections
ms.assetid: 73ee8171-3379-4384-bfc8-071b3eebbc8f
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7b0e2b4020f3f9d27be84c1a6dc2f0944da88f5f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="connect-to-analysis-services"></a>连接到 Analysis Services
  使用本部分中的信息，了解连接字符串属性、用于连接的客户端库、Analysis Services 支持哪些身份验证方法以及如何在使用脱机服务器前设置或清除连接。  
  
## <a name="analysis-services-connections"></a>Analysis Services 连接  
 Analysis Services 使用 TCP 作为网络协议，使用 XML for Analysis (XMLA) 作为通信协议。 在最底层，与 Analysis Services 一起提供的所有客户端库都实现了 XMLA-over-TCP。 尽管可以基于原始 XMLA 生成应用程序，但是大多数应用程序和应用程序开发人员都使用客户端库以利用它们提供的对象模型和代码编写效率。 对于客户端与 Analysis Services 的连接，如果无法跨堆栈使用 TCP，则可以使用 IIS 作为中间连接。 通过 IIS 使用 HTTP 访问的一个优点就是，能够从传递连接字符串上凭据的应用程序连接。  
  
 涉及连接性的所有讨论通常包括身份验证。 与其他 SQL Server 功能不同，Analysis Services 仅使用 Windows 凭据。 不能在 Analysis Services 的后端连接上使用 SQL Server 数据库身份验证、声明身份验证、基于窗体的身份验证或摘要。 本节中将提供有关身份验证的更多信息。  
  
##  <a name="bkmk_clientApps"></a> 连接任务  
  
|链接|任务说明|  
|----------|----------------------|  
|[从客户端应用程序进行连接 (Analysis Services)](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)|如果您不熟悉 Analysis Services，请查看本主题以开始了解最常与 Analysis Services 一起使用的工具和应用程序。|  
|[连接字符串属性 (Analysis Services)](../../analysis-services/instances/connection-string-properties-analysis-services.md)|Analysis Services 包含各种服务器和数据库属性，允许您为特定应用程序自定义连接，而不管实例或数据库是如何配置的。|  
|[Analysis Services 支持的身份验证方法](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)|本主题简要介绍了 Analysis Services 使用的身份验证方法。|  
|[针对 Kerberos 约束委派对 Analysis Services 进行配置](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)|很多商业智能解决方案需要模拟以确保仅将授权的数据返回给每个用户。 在本主题中，您将了解使用模拟的要求。 本主题还介绍配置 Analysis Services 以使用 Kerberos 约束委托的步骤。|  
|[针对 Analysis Services 实例的 SPN 注册](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)|Kerberos 身份验证要求在多服务器解决方案中模拟或委托用户标识的服务具有有效的服务主体名称 (SPN)。 使用本主题中的信息以了解如何进行 Analysis Services 的 SPN 注册。|  
|[在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|基本身份验证或跨域边界是针对 HTTP 访问配置 Analysis Services 的两个重要原因。|  
|[用于 Analysis Services 连接的数据访问接口](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)|Analysis Services 提供用于访问服务器操作或 Analysis Services 数据的三个客户端库。 本主题简要介绍了 ADOMD.NET、Analysis Services 管理对象 (AMO) 和 Analysis Services OLE DB 访问接口 (MSOLAP)。|  
|[断开 Analysis Services 服务器上用户和会话的连接](../../analysis-services/instances/disconnect-users-and-sessions-on-analysis-services-server.md)|在使服务器脱机或执行基线性能测试前清除现有连接和会话。|  
  
## <a name="see-also"></a>另请参阅  
 [安装后配置 (Analysis Services)](../../analysis-services/instances/post-install-configuration-analysis-services.md)   
 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
  
  
