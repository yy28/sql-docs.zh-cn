---
title: 在报表服务器上配置基本身份验证 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 34ef8153b717c13b6fc5fdf2147b90339f8640e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242770"
---
# <a name="configure-basic-authentication-on-the-report-server"></a>在报表服务器上配置基本身份验证
  默认情况下，Reporting Services 接受指定 Negotiate 和 NTLM 身份验证的请求。 如果部署中包括使用基本身份验证的客户端应用程序或浏览器，则必须将基本身份验证添加到支持的类型列表中。 此外，若要使用报表生成器，必须启用对报表生成器文件的匿名访问。  
  
 若要对报表服务器配置基本身份验证，则需要在 RSReportServer.config 文件中编辑 XML 元素和值。 可以复制并粘贴本主题中的示例来替换默认值。  
  
 启用基本身份验证之前，请验证您的安全基础结构是否支持。 在基本身份验证模式下，报表服务器 Web 服务会将凭据传递给本地安全机构。 如果凭据指定本地用户帐户，则该用户将由报表服务器计算机上的本地安全机构进行身份验证，并获取对本地资源有效的安全令牌。 域用户帐户的凭据将转发给域控制器并由它进行身份验证。 生成的票证对网络资源有效。  
  
 若要在将凭据传输到网络中的域控制器时降低凭据被截获的风险，则需要通道加密，如安全套接字层 (SSL)。 基本身份验证本身以明文形式传输用户名，以 Base-64 编码格式传输密码。 添加信道加密会使数据包不可读。 有关详细信息，请参阅 [配置本机模式报表服务器上的 SSL 连接](configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
 启用基本身份验证后，请注意在将连接属性设置为向报表提供数据的外部数据源时，用户不能选择 **“Windows 集成安全性”** 选项。 该选项将在数据源属性页中显示为灰色。  
  
> [!NOTE]  
>  以下说明针对本机模式报表服务器。 如果在 SharePoint 集成模式下部署报表服务器，则必须使用指定 Windows 集成安全性的默认身份验证设置。 报表服务器使用默认 Windows 身份验证扩展插件中的内部功能支持 SharePoint 集成模式下的报表服务器。  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>将报表服务器配置为使用基本身份验证  
  
1.  在文本编辑器中打开 RSReportServer.config。  
  
     该文件位于*\<驱动器 >:* \Program Files\Microsoft SQL Server\MSRS12。MSSQLSERVER\Reporting Services\ReportServer。  
  
2.  查找 <`Authentication`>。  
  
3.  复制以下最能满足您需要的一个 XML 结构。 第一个 XML 结构提供了用于指定所有元素的占位符，将在下一部分对这些元素进行介绍：  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsBasic>  
                       <LogonMethod>3</LogonMethod>  
                       <Realm></Realm>  
                       <DefaultDomain></DefaultDomain>  
                 </RSWindowsBasic>  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     如果使用的是默认值，则可复制最小元素结构：  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsBasic/>  
          </AuthenticationTypes>  
    ```  
  
4.  将它粘贴到的现有条目 <`Authentication`>。  
  
     如果使用的是多个身份验证类型，则只能添加 `RSWindowsBasic` 元素，而不能删除 `RSWindowsNegotiate`、`RSWindowsNTLM` 或 `RSWindowsKerberos` 的条目。  
  
     若要支持 Safari 浏览器，则不能将报表服务器配置为使用多个身份验证类型。 必须仅指定 `RSWindowsBasic`，并删除其他条目。  
  
     请注意，不能将 `Custom` 与其他身份验证类型一起使用。  
  
5.  空值替换为 <`Realm`> 或 <`DefaultDomain`> 对您环境有效的值。  
  
6.  保存该文件。  
  
7.  如果配置了扩展部署，请对该部署中的其他报表服务器重复这些步骤。  
  
8.  重新启动报表服务器以清除当前打开的任何会话。  
  
## <a name="rswindowsbasic-reference"></a>RSWindowsBasic 引用  
 配置基本身份验证时，可以指定以下元素。  
  
|元素|Required|有效值|  
|-------------|--------------|------------------|  
|LogonMethod|是<br /><br /> 如果不指定值，将使用 3。|`2` = 网络登录，针对要对纯文本密码进行身份验证的高性能服务器。<br /><br /> `3` = 明文登录，在此情况下，登录凭据保留在随各 HTTP 请求一起发送的身份验证包中，这样，该服务器在连接到网络中的其他服务器时可以模拟该用户。 （默认值）<br /><br /> 注意：中不支持值 0 （针对交互登录） 和 1 （针对批处理登录） [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]。|  
|领域|可选|指定包含授权和身份验证功能的资源分区，这些功能用于控制对组织中受保护资源的访问。|  
|默认域|可选|指定服务器用来对用户进行身份验证的域。 此值是可选的。但如果忽略此值，报表服务器会将计算机名称用作域。 如果计算机是域的成员，则该域是默认域。 如果在域控制器上安装了报表服务器，则所用的域为该计算机控制的域。|  
  
## <a name="enabling-anonymous-access-to-report-builder-application-files"></a>启用对报表生成器应用程序文件的匿名访问  
 报表生成器使用 ClickOnce 技术下载其应用程序文件，并在客户端计算机上安装这些文件。 当客户端计算机启动 ClickOnce 应用程序时，ClickOnce 应用程序启动程序将发出对报表服务器计算机上的其他应用程序文件的请求。 如果将报表服务器配置为使用基本身份验证，则 ClickOnce 应用程序启动程序将无法进行身份验证检查，因为它不支持基本身份验证。  
  
 可通过配置对报表生成器程序文件的匿名访问来解决此问题。 这样做可使 ClickOnce 在检索其文件时绕过身份验证检查。 请执行以下操作启用匿名访问：  
  
-   验证报表服务器是否已配置为使用基本身份验证。  
  
-   在 ReportBuilder 下创建 Bin 文件夹，然后将 4 个程序集复制到文件夹中。  
  
-   将 `IsReportBuilderAnonymousAccessEnabled` 元素添加到 RSReportServer.config，并将其设置为 `True`。 保存该文件后，报表服务器将创建报表生成器的新端点。 该端点将内部用于访问程序文件，并且不具有可在代码中使用的编程接口。 具有不同的端点可使报表生成器在报表服务器服务进程边界中其自己的应用程序域中运行。  
  
-   还可以指定最低特权帐户以在与报表服务器不同的安全上下文下处理请求。 此帐户将成为匿名帐户，用于访问报表服务器上的报表生成器文件。 该帐户在 ASP.NET 工作进程中设置线程的标识。 该线程中运行的请求会被传递到报表服务器，而不进行身份验证检查。 此帐户等效于使用 IUSR_\<计算机 > 时启用匿名访问和模拟进程帐户在 Internet 信息服务 (IIS)，用于设置 ASP.NET 工作线程的安全上下文。 若要指定该帐户，需要将其添加到报表生成器 Web.config 文件中。  
  
 若要启用对报表生成器程序文件的匿名访问，必须将报表服务器配置为使用基本身份验证。 如果未将报表服务器配置为使用基本身份验证，在尝试启用匿名访问时，将收到一个错误。  
  
 有关身份验证问题和报表生成器的详细信息，请参阅[配置报表生成器访问权限](../report-server/configure-report-builder-access.md)。  
  
#### <a name="to-configure-report-builder-access-on-a-report-server-configured-for-basic-authentication"></a>在配置为使用基本身份验证的报表服务器上配置报表生成器访问  
  
1.  通过检查 RSReportServer.config 文件中的身份验证设置来验证报表服务器是否配置为使用基本身份验证。  
  
2.  在 ReportBuilder 文件夹下创建一个 BIN 文件夹。 默认情况下，该文件夹位于 \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\ReportBuilder。  
  
3.  将以下程序集从 ReportServer\Bin 文件夹复制到 ReportBuilder\BIN 文件夹中：  
  
     Microsoft.ReportingServices.Diagnostics.dll  
  
     Microsoft.ReportingServices.Interfaces.dll  
  
     ReportingServicesAppDomainManager.dll  
  
     RSHttpRuntime.dll  
  
4.  还可以创建一个 Web.config 文件以在匿名帐户下处理报表生成器请求：  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
    <system.web>  
    <authentication mode="Windows" />    
    <identity impersonate="true " userName="username" password="password"/>  
    </system.web>  
    </configuration>  
    ```  
  
     如果包含一个 Web.config 文件，则必须将身份验证模式设置为 `Windows`。  
  
     `Identity impersonate` 可以是 `True` 或 `False`。  
  
    -   如果不希望 ASP.NET 读取安全令牌，则将它设置为 `False`。 该请求将在报表服务器服务的安全上下文中运行。  
  
    -   如果希望 ASP.NET 从宿主层读取安全令牌，则将它设置为 `True`。 如果设置为 `True`，还必须指定 `userName` 和 `password` 来指定一个匿名帐户。 您指定的凭据将确定发出请求时所处的安全上下文。  
  
5.  将 Web.config 文件保存到 ReportBuilder\bin 文件夹。  
  
6.  打开 RSReportServer.config 文件，在“Services”部分中查找 `IsReportManagerEnabled`，然后在其下添加以下设置：  
  
    ```  
    <IsReportBuilderAnonymousAccessEnabled>True</IsReportBuilderAnonymousAccessEnabled>  
    ```  
  
7.  保存 RSReportServer.config 并关闭该文件。  
  
8.  重新启动报表服务器。  
  
## <a name="see-also"></a>请参阅  
 [报表服务器应用程序的应用程序域](../report-server/application-domains-for-report-server-applications.md)   
 [Reporting Services 安全性和保护](reporting-services-security-and-protection.md)  
  
  
