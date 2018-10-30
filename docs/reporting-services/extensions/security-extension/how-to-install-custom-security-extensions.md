---
title: 如何安装自定义安全扩展插件 | Microsoft Docs
ms.date: 07/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 853d40be782355841d68d3ace92e4228b0631057
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50020661"
---
# <a name="how-to-install-custom-security-extensions"></a>如何安装自定义安全扩展插件

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016 引入了一个新的 Web 门户以托管新的 Odata API，并也托管新的报表工作负载，例如移动报表和 KPI。 此新门户依赖于更新的技术，并通过在单独的进程中运行与熟悉的 ReportingServicesService 分隔开来。 此进程不是 ASP.NET 托管的应用程序，因此中断了现有自定义安全扩展插件中的假设。 此外，自定义安全扩展插件的当前接口不允许传入任何外部上下文，留给实现者唯一的选择来检查熟知的全局 ASP.NET 对象，这要求对接口进行一些更改。

## <a name="what-changed"></a>有何更改？

引入了可实现的一个新接口，此接口提供一个 IRSRequestContext，提供扩展插件用于做出与身份验证相关决定的更常见属性。

在以前的版本中，报表管理器位于前端，并且可以使用其自定义登录页面进行配置。 在 Reporting Services 2016 中，仅支持 reportserver 托管的一个页面，并且应对两个应用程序都进行身份验证。

## <a name="implementation"></a>实现

在以前的版本中，扩展可依赖于常见假设，即 ASP.NET 对象随时可用。 由于新门户不在 ASP.NET 中运行，因此，扩展可能会遇到对象为 NULL 的问题。

大多数泛型示例访问 HttpContext.Current 来读取如标头和 Cookie 等请求的信息。 为了使扩展插件能够做出相同的决策，我们在提供请求信息的扩展中引入了一个新方法，并在从门户进行身份验证时调用该方法。 

扩展插件必须实现 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> 接口才能利用此方法。 扩展插件需要实现 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> 方法的两个版本，正如 reportserver 上下文所调用的方法，以及其他在 webhost 进程中所使用的方法。 以下示例展示了此门户的一个简单实现，其中使用了 reportserver 解析的标识。

``` 
public void GetUserInfo(IRSRequestContext requestContext, out IIdentity userIdentity, out IntPtr userId)
{
    userIdentity = null;
    if (requestContext.User != null)
    {
        userIdentity = requestContext.User;
    }

    // initialize a pointer to the current user id to zero
    userId = IntPtr.Zero;
}
```

## <a name="deployment-and-configuration"></a>部署和配置

自定义安全扩展插件所需的基本配置与以前的版本相同。 需要对 web.config 和 rsreportserver.config 进行更改：有关详细信息，请参阅[在 Report Server 上配置自定义身份验证或窗体身份验证](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)。

报表管理器不再具有单独的 web.config，此门户将继承与 reportserver 终结点相同的设置。

## <a name="machine-keys"></a>计算机密钥

对于需要对身份验证 Cookie 进行解密的窗体身份验证，需要使用相同的计算机密钥和解密算法对这两个进程进行配置。 对于那些以前设置了 Reporting Services 以在扩展环境中工作的人来说，这是一个熟悉的步骤，但现在即使在单台计算机上进行部署，这也成为了必要步骤。

你应该使用特定于部署的验证密钥，可使用一些工具来生成密钥，例如 Internet Information Services 管理器 (IIS)。 在 Internet 上可以找到其他工具。

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 和更高版本

**\ReportServer\rsReportServer.config**

在 `<configuration>` 下添加。

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

在 `<system.web>` 下添加。
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

在 `<configuration>` 下添加。

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Power BI 报表服务器

这是 2017 年 6 月发布的版本（内部版本 14.0.600.301）。

**\ReportServer\rsReportServer.config**

在 `<configuration>` 下添加。

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>配置 Passthrough Cookie

新门户和 reportserver 使用内部的 soap API 进行通信以执行其某些操作（类似于之前版本的报表管理器）。 当需要将其他 Cookie 从门户传递到服务器时，PassThroughCookies 属性仍然可用。 有关详细信息，请参阅[配置 Web 门户以传递自定义身份验证 Cookie](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)。

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="next-steps"></a>后续步骤

[在报表服务器上配置自定义身份验证或窗体身份验证](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[配置报表管理器以便传递自定义身份验证 Cookie](../../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
