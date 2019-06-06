---
title: 保护 RDS 应用程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b2afe6074f115c1d9770251c51e6288e9d92ee3b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699333"
---
# <a name="securing-rds-applications"></a>保证 RDS 应用程序的安全
本主题提供了 rds.的安全信息  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer 的安全问题  
 具有新安全增强功能添加到 Microsoft Internet Explorer，某些 ADO 和 RDS 对象被限制为仅在"安全"模式环境中运行。 这将要求您了解这些问题，包括不同的区域、 安全级别、 限制行为、 不安全的操作，并自定义的安全设置。  
  
## <a name="security-and-your-web-server"></a>安全和 Web 服务器  
 如果您使用[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象 Internet Web 服务器上，请记住，这样做可以创建潜在的安全风险。 获取有效的数据源名称 (DSN)、 用户 ID 和密码信息的外部用户可以编写将发送到该数据源的任何查询的页面。 如果你想对数据源的更受限制的访问，一种选择是取消注册，删除**提高**对象 (msadcf.dll)，并改为使用硬编码查询中使用自定义业务对象。  
  
 使用提高对象的安全隐患的详细信息，请在 Microsoft 安全网站上参阅 Microsoft 安全公告 MS99-025。  
  
## <a name="client-impersonation-and-security"></a>客户端模拟和安全性  
 如果**密码身份验证**IIS Web 服务器属性设置为 （适用于 Windows NT 4.0) 的 Windows NT 质询/响应身份验证或集成 Windows 身份验证 （适用于 Windows 2000)，则业务对象调用客户端的安全上下文。 这是允许通过 HTTP 的客户端模拟的 RDS 1.5 中的新功能。 在此模式下工作时，登录到 Web 服务器 (IIS) 不是匿名的但使用的用户 ID 和客户端计算机下运行的密码。 如果 ODBC Dsn 设置了要使用可信连接进行连接，然后访问数据库，如 SQL Server，也恰好在客户端的安全上下文中。 但这仅适用于该数据库位于 IIS; 所在的计算机上客户端凭据不能结转到另一个计算机。  
  
 例如，客户端，John Doe userid ="JohnD"和密码 ="机密"登录到客户端计算机上。 他运行需要访问的基于浏览器的应用程序**提高**对象来创建[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)通过执行 SQL 查询"MyServer"计算机上运行 IIS。 MyServer，运行 Windows NT Server 4.0 的系统设置为使用 Windows NT 质询/响应身份验证、 其 ODBC DSN 具有"使用可信连接进行连接"选择，并且服务器还包含 SQL Server 数据源。 Web 服务器上收到请求时，它会要求提供用户 ID 和密码的客户端。 因此，请求登录 MyServer 为来自"JohnD"/"机密"而不是 IUSER_MyServer （这是默认值上匿名密码身份验证时）。 同样，在登录到 SQL Server，"JohnD"时使用"机密"/。  
  
 因此，IIS Windows NT 质询/响应身份验证模式允许的 HTML 页以创建不提示用户的显式登录到数据库所需的用户 ID 和密码信息。 如果使用了 IIS 基本身份验证，则这还将需要。  
  
## <a name="password-authentication"></a>密码身份验证  
 RDS 可以与运行中的三种的密码身份验证模式的任何一个的 IIS Web 服务器进行通信：Anonymous、 Basic 或 NT 质询/响应身份验证 （在 Windows 2000 中称为集成 Windows 身份验证）。 这些设置用于定义 Web 服务器如何控制通过它，例如，要求客户端计算机在 NT Web 服务器上具有明确的访问权限的访问权限。


