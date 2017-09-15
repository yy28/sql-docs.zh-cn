---
title: "保护 RDS 应用程序 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 72a46915beed5bb65953788b2b1b7283d90cb8e5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="securing-rds-applications"></a>保护 RDS 应用程序
本主题提供 rds.的安全信息  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer 安全问题  
 借助新增安全增强功能添加到 Microsoft Internet Explorer，某些 ADO 和 RDS 对象被限制为仅在"安全"模式环境中运行。 这要求你知道这些问题，包括不同的区域、 安全级别，限制行为、 不安全的操作，并自定义安全设置。  
  
## <a name="security-and-your-web-server"></a>安全和你的 Web 服务器  
 如果你使用[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象上你的 Internet Web 服务器，请记住，这样做会产生潜在的安全风险。 获取有效的数据源名称 (DSN)、 用户 ID 和密码信息的外部用户无法将页将任何查询发送到该数据源写入。 如果你想对数据源的更受限制的访问，一个选项是撤消注册并删除**提高**对象 (msadcf.dll)，并改为使用硬编码的查询中使用自定义业务对象。  
  
 使用提高对象的安全隐患的详细信息，请参阅 Microsoft 安全公告 MS99-025 上 Microsoft Security 网站。  
  
## <a name="client-impersonation-and-security"></a>客户端模拟和安全  
 如果**密码身份验证**IIS Web 服务器的属性设置为 Windows NT 质询/响应 （适用于 Windows NT 4.0) 的身份验证或集成 Windows 身份验证 （用于 Windows 2000)，则将业务对象客户端的安全上下文中调用。 这是允许通过 HTTP 的客户端模拟的 RDS 1.5 中的新功能。 在此模式下工作时，登录到 Web 服务器 (IIS) 不是匿名的但使用的用户 ID 和客户端计算机运行下的密码。 如果 ODBC Dsn 设置为使用可信连接，然后访问数据库，如 SQL Server，也会发生在客户端的安全上下文。 但是这仅适用如果数据库位于同一台计算机作为 IIS;客户端凭据无法转入尚未另一台计算机。  
  
 例如，客户端，John Doe userid ="JohnD"和密码 ="密码"登录到客户端计算机上。 他运行的基于浏览器的应用程序需要访问**提高**对象以创建[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)通过执行 SQL 查询"MyServer"计算机上运行 IIS。 MyServer，运行 Windows NT Server 4.0 的系统设置为使用 Windows NT 质询/响应身份验证、 其 ODBC DSN 具有"使用受信任连接"选择，且服务器还包含 SQL Server 数据源。 当在 Web 服务器上收到请求时，它会要求提供用户 ID 和密码的客户端。 因此，请求登录 MyServer 作为来自"JohnD"/"机密"而不是 IUSER_MyServer （这是默认值上匿名密码身份验证时）。 同样，当登录到 SQL Server，"JohnD"/"机密"使用。  
  
 因此，IIS Windows NT 质询/响应身份验证模式允许的 HTML 页以创建没有显式提示用户输入登录到数据库所需的用户 ID 和密码信息。 如果使用了 IIS 基本身份验证，则这还应必需。  
  
## <a name="password-authentication"></a>密码身份验证  
 RDS 可以与在任何一个的三种的密码身份验证模式中运行的 IIS Web 服务器进行通信： 匿名、 基本，或 NT 质询/响应身份验证 （在 Windows 2000 中称为集成 Windows 身份验证）。 这些设置用于定义 Web 服务器如何控制通过它，例如要求客户端计算机在 NT Web 服务器上具有明确的访问权限的访问。



