---
title: 建立在 ADOMD.NET 中的安全连接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- connections [ADOMD.NET]
- security [ADOMD.NET]
ms.assetid: b084d447-1456-45a4-8e0e-746c07d7d6fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b77fefaad8ac573e526412f1c81be3969743a3a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178207"
---
# <a name="establishing-secure-connections-in-adomdnet"></a>在 ADOMD.NET 中建立安全连接
  在 ADOMD.NET 中使用连接时，连接所用的安全方法取决于调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 方法时所使用的连接字符串的 `ProtectionLevel` 属性的值。  
  
 `ProtectionLevel` 属性提供的安全级别有四种：不要求身份验证、要求身份验证、签名、加密。 下表介绍这些不同的安全级别。  
  
> [!NOTE]  
>  如果选择使用数据库连接池，数据库将无法管理安全性。 这是因为数据库连接池要求连接字符串与池连接相同。 因此，您必须在其他位置管理安全性。  
  
|安全级别|ProtectionLevel 值|  
|--------------------|---------------------------|  
|*未经身份验证的连接*<br /> 不要求身份验证的连接不会进行任何形式的身份验证。 这种连接是最普遍支持的连接，但同时也是最不安全的连接。|`None`|  
|*经过身份验证的连接*<br /> 要求身份验证的连接会对进行连接的用户进行身份验证，但是不保证其他通信的安全。 这种连接颇为有用，因为您可为连接到分析数据源的用户或应用程序建立标识。|`Connect`|  
|*签名的连接*<br /> 签名连接会对请求连接的用户进行身份验证，而且确保传输不会被修改。 在必须验证传输数据的真实性时，这种连接非常有用。 但签名连接仅可防止数据包的内容被修改。 在传递的过程中仍可查看这些内容。 **注意：** 签名的连接仅支持 xml for Analysis 访问接口提供[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|`Pkt Integrity` 或 `PktIntegrity`|  
|*加密的连接*<br /> 加密连接是 ADOMD.NET 使用的默认连接类型。 这种连接会对请求连接的用户进行身份验证，还会对所传输的数据进行加密。 加密连接是 ADOMD.NET 可创建的最安全的连接形式。 数据包的内容不能被查看或修改，因而可以使数据在传输过程中得到保护。 **注意：** 加密的连接仅支持 xml for Analysis 访问接口提供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|`Pkt Privacy` 或 `PktPrivacy`|  
  
 但是，并非所有类型的连接都可使用全部安全级别：  
  
-   TCP 连接可以使用这四种安全级别中的任意一种。 实际上，在与 Windows 集成安全性一起使用时，TCP 连接可提供最安全的连接分析数据源的方法。  
  
-   HTTP 连接只能是要求身份验证的连接。 因此，`ProtectionLevel` 属性必须设置为 `Connect`。  
  
-   HTTPS 连接只能是加密连接。 因此 `ProtectionLevel` 属性必须设置为 `Pkt Privacy` 或 `PktPrivacy`。  
  
## <a name="securing-tcp-connections"></a>保护 TCP 连接的安全  
 对于 TCP 连接，`ProtectionLevel` 属性支持所有四种安全级别，如下表所示。  
  
|ProtectionLevel 值|是否用于 TCP 连接？|结果|  
|---------------------------|------------------------------|-------------|  
|`None`|用户帐户控制|指定不要求身份验证的连接。<br /><br /> TCP 流从访问接口请求，但是不会对请求该流的用户执行任何形式的身份验证。|  
|`Connect`|用户帐户控制|指定要求身份验证的连接。<br /><br /> TCP 流的请求从提供程序，以及然后请求该流的用户的安全上下文进行身份验证对服务器：<br /><br /> -如果验证成功，则不执行任何其他操作。<br />-如果身份验证失败，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>对象从多维数据源断开连接，并引发异常。<br /><br /> 验证成功或失败后，会释放用于验证该连接的安全上下文。|  
|`Pkt Integrity` 或 `PktIntegrity`|用户帐户控制|指定签名连接。<br /><br /> TCP 流的请求从提供程序，以及然后请求该流的用户的安全上下文进行身份验证对服务器：<br /><br /> -如果验证成功，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>对象关闭现有 TCP 流，然后打开已签名的 TCP 流来处理所有请求。 对数据或元数据的每一请求都会使用打开连接时所用的安全上下文进行身份验证。 另外，对每个包都进行数字签名，以确保 TCP 包的负载没有经过任何方式的更改。<br />-如果身份验证失败，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>对象从多维数据源断开连接，并引发异常。|  
|`Pkt Privacy` 或 `PktPrivacy`|用户帐户控制|指定加密连接。 **注意：** 还可以通过不设置指定的加密的连接`ProtectionLevel`连接字符串中的属性。 <br /><br /> TCP 流从访问接口请求，然后在服务器上对请求该流的用户的安全上下文进行身份验证：<br /><br /> -如果验证成功，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>对象关闭现有 TCP 流，并打开加密的 TCP 流来处理所有请求。 对数据或元数据的每一请求都会使用打开连接时所用的安全上下文进行身份验证。 另外，每一 TCP 包的负载都会使用该访问接口和多维数据源都支持的最高级别加密方法进行加密。<br />-如果身份验证失败，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>对象从多维数据源断开连接，并引发异常。|  
  
### <a name="using-windows-integrated-security-for-the-connection"></a>对连接使用 Windows 集成安全性  
 Windows 集成安全性是建立和保护与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的连接的最安全方式。 Windows 集成安全性不会在身份验证过程中泄露安全凭据，如用户名或密码，而是使用当前运行进程的安全标识符来确立标识。 对于大多数客户端应用程序，此安全标识符代表当前登录用户的标识。  
  
 若要使用 Windows 集成安全性，连接字符串需要以下设置：  
  
-   对于 `Integrated Security` 属性，不设置此属性，或者将此属性设置为 `SSPI`。  
  
    > [!NOTE]  
    >  Windows 集成安全性仅可用于 TCP 连接，因为 HTTP 连接必须使用 `Basic` 属性的 `Integrated Security` 设置。  
  
-   对于 `ProtectionLevel` 属性，请将此属性设置为 `Connect`、`Pkt Integrity` 或 `Pkt Privacy`。  
  
## <a name="securing-http-connections"></a>保护 HTTP 连接的安全  
 HTTPS 和安全套接字层 (SSL) 可用于从外部保护与分析数据源之间的 HTTP 通信。  
  
 因为 XMLA 访问接口仅使用安全 HTTP，所以 ADOMD.NET 中的 HTTP 连接必须是签名连接，如下表所示。  
  
|ProtectionLevel 值|用于 HTTP 还是 HTTPS|  
|---------------------------|----------------------------|  
|`None`|否|  
|`Connect`|HTTP|  
|`Pkt Integrity` 或 `PktIntegrity`|否|  
|`Pkt Privacy` 或 `PktPrivacy`|HTTPS|  
  
### <a name="opening-a-secure-http-connection"></a>打开安全 HTTP 连接  
 下面的示例演示如何使用 ADOMD.NET 打开 `AdventureWorksAS` 示例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的 HTTP 连接：  
  
```vb  
Public Function GetAWEncryptedConnection( _  
    Optional ByVal serverName As String = "https:\\localhost\isapy\msmdpump.dll") _  
    As AdomdConnection  
  
    Dim strConnectionString As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' To establish an encrypted connection, set the   
        ' ProtectionLevel setting to PktPrivacy.  
        strConnectionString = "DataSource=" & serverName & ";" & _  
            "Catalog=AdventureWorksAS;" & _  
            "ProtectionLevel=PktPrivacy;"  
  
        ' Note that username and password are not supplied here.  
        ' The current security context is used for authentication  
        ' purposes.  
  
        objConnection.ConnectionString = strConnectionString  
        objConnection.Open()  
    Catch ex As Exception  
        objConnection = Nothing  
        Throw ex  
    Finally  
        ' Return the encrypted connection.  
        GetAWEncryptedConnection = objConnection  
    End Try  
End Function  
  
```  
  
## <a name="see-also"></a>请参阅  
 [在 ADOMD.NET 中建立连接](connections-in-adomd-net.md)  
  
  
