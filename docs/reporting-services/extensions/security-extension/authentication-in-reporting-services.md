---
title: "Reporting Services 中的身份验证 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], authentication
- forms-based authentication [Reporting Services]
- authentication [Reporting Services]
- custom authentication [Reporting Services]
ms.assetid: 103ce1f9-31d8-44bb-b540-2752e4dcf60b
caps.latest.revision: 25
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 6926d7787a715ab9183763939ca78ed192d0e251
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="authentication-in-reporting-services"></a>Reporting Services 中的身份验证
  身份验证是确立用户对某一身份的权限的过程。 您可以使用多种方法来验证某一用户的身份。 最常见的方法是使用密码。 例如，在实现窗体身份验证时，您希望某一实现查询用户的凭据（通常通过请求提供登录名和密码的某些界面），然后根据数据存储区（例如数据库表或配置文件）验证用户。 如果无法验证凭据，该身份验证过程将失败，并且用户将假定匿名身份。  
  
## <a name="custom-authentication-in-reporting-services"></a>Reporting Services 中的自定义身份验证  
 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中，Windows 操作系统通过集成的安全性或通过用户凭据的显式接受和验证，处理用户的身份验证。 可以在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中开发自定义身份验证，以支持附加的身份验证架构。 这可以通过安全扩展插件接口 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> 实现。 所有扩展插件都继承自报表服务器部署和使用的任何扩展插件的 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 基接口。 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 以及 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> 是 <xref:Microsoft.ReportingServices.Interfaces> 命名空间的成员。  
  
 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中对报表服务器进行身份验证的主要方式是 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 方法。 此 Reporting Services Web 服务成员可用于将用户凭据传递到某一报表服务器以进行验证。 你的基础安全扩展实现**IAuthenticationExtension2.LogonUser**其中包含自定义身份验证代码。 在窗体身份验证示例中， **LogonUser**，其数据库中执行针对提供的凭据和一个自定义用户存储进行身份验证检查。 实现的一个示例**LogonUser**如下所示：  
  
```  
public bool LogonUser(string userName, string password, string authority)  
{  
   return AuthenticationUtilities.VerifyPassword(userName, password);  
}  
  
```  
  
 以下示例函数用于验证提供的凭据：  
  
```  
  
internal static bool VerifyPassword(string suppliedUserName,  
   string suppliedPassword)  
{   
   bool passwordMatch = false;  
   // Get the salt and pwd from the database based on the user name.  
   // See "How To: Use DPAPI (Machine Store) from ASP.NET," "How To:  
   // Use DPAPI (User Store) from Enterprise Services," and "How To:  
   // Create a DPAPI Library" for more information about how to use  
   // DPAPI to securely store connection strings.  
   SqlConnection conn = new SqlConnection(  
      "Server=localhost;" +   
      "Integrated Security=SSPI;" +  
      "database=UserAccounts");  
   SqlCommand cmd = new SqlCommand("LookupUser", conn);  
   cmd.CommandType = CommandType.StoredProcedure;  
  
   SqlParameter sqlParam = cmd.Parameters.Add("@userName",  
       SqlDbType.VarChar,  
       255);  
   sqlParam.Value = suppliedUserName;  
   try  
   {  
      conn.Open();  
      SqlDataReader reader = cmd.ExecuteReader();  
      reader.Read(); // Advance to the one and only row  
      // Return output parameters from returned data stream  
      string dbPasswordHash = reader.GetString(0);  
      string salt = reader.GetString(1);  
      reader.Close();  
      // Now take the salt and the password entered by the user  
      // and concatenate them together.  
      string passwordAndSalt = String.Concat(suppliedPassword, salt);  
      // Now hash them  
      string hashedPasswordAndSalt =  
         FormsAuthentication.HashPasswordForStoringInConfigFile(  
         passwordAndSalt,  
         "SHA1");  
      // Now verify them. Returns true if they are equal.  
      passwordMatch = hashedPasswordAndSalt.Equals(dbPasswordHash);  
   }  
   catch (Exception ex)  
   {  
       throw new Exception("Exception verifying password. " +  
          ex.Message);  
   }  
   finally  
   {  
       conn.Close();  
   }  
   return passwordMatch;  
}  
```  
  
## <a name="authentication-flow"></a>身份验证流程  
 Reporting Services Web 服务提供了自定义身份验证扩展插件的 web 门户和报表服务器启用窗体身份验证。  
  
 Reporting Services Web 服务的 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 方法用于将凭据提交到报表服务器以供身份验证。 该 Web 服务使用 HTTP 标头将身份验证票证（通称为“cookie”）从服务器传递到客户端，以便用于已验证的登录请求。  
  
 下图描述了在您使用配置为使用自定义身份验证扩展插件的报表服务器部署应用程序时，向该 Web 服务验证用户身份的方法。  
  
 ![Reporting Services 安全身份验证流](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionauthenticationflow.gif "Reporting Services 安全身份验证流")  
  
 如图 2 中所示，该身份验证流程如下：  
  
1.  客户端应用程序调用 Web 服务 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 方法以便验证某一用户的身份。  
  
2.  Web 服务方法调用了<xref:ReportService2010.ReportingService2010.LogonUser%2A>方法的安全扩展，具体而言，实现的类**IAuthenticationExtension2**。  
  
3.  您的 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 实现验证用户存储或安全机构中的用户名和密码。  
  
4.  在成功进行身份验证后，该 Web 服务将创建一个 cookie 并为会话管理它。  
  
5.  该 Web 服务将该身份验证票证返回到调用应用程序的 HTTP 标头上。  
  
 在该 Web 服务成功通过安全扩展插件验证用户身份后，它将生成用于后续请求的 cookie。 该 cookie 可能不会在自定义安全机构内持久化，因为报表服务器不拥有该安全机构。 该 cookie 从 <xref:ReportService2010.ReportingService2010.LogonUser%2A> Web 服务方法返回并且用于后续的 Web 服务方法调用和 URL 访问中。  
  
> [!NOTE]  
>  为了避免在传输期间损坏 cookie，从 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 返回的身份验证 cookie 应使用安全套接字层 (SSL) 加密安全地传输。  
  
 如果您在安装自定义安全扩展插件时通过 URL 访问报表服务器，则 Internet 信息服务 (IIS) 和 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 将自动管理身份验证票证的传输。 如果您在通过 SOAP API 访问报表服务器，则您的代理类的实现必须包括用于管理身份验证票证的附加支持。 有关使用 SOAP API 和管理身份验证票证的详细信息，请参阅“使用具有自定义安全性的 Web 服务”。  
  
## <a name="forms-authentication"></a>窗体身份验证  
 窗体身份验证是一种 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 身份验证，其中，未经身份验证的用户定向到某一 HTML 窗体。 一旦用户提供凭据后，系统将发出包含身份验证票证的 cookie。 对于以后的请求，系统首先检查 cookie 以确定报表服务器是否已验证用户的身份。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 可以扩展，以便使用可通过 Reporting Services API 提供的安全可扩展接口支持窗体身份验证。 如果您扩展 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 以使用窗体身份验证，则将安全套接字层 (SSL) 用于与报表服务器的全部通信，以便防止恶意用户获取对其他用户的 cookie 的访问。 SSL 使客户端和报表服务器能够彼此进行身份验证，并且确保没有其他计算机可以读取两台计算机之间的通信内容。 通过 SSL 连接从客户端传送的所有数据都进行加密，以便恶意用户无法截获发送给报表服务器的密码或数据。  
  
 实现窗体身份验证通常是为了支持针对非 Windows 的其他平台的帐户和身份验证。 向请求对某一报表服务器的访问的用户提供一个图形界面，并且提供的凭据将提交到安全机构以便进行身份验证。  
  
 窗体身份验证要求某一人输入凭据。 对于直接与 Reporting Services Web service 服务通信的无人参与应用程序，窗体身份验证必须与自定义身份验证架构相结合。  
  
 在以下情况下窗体身份验证适用于 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]：  
  
-   您需要存储不具有 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帐户的用户并验证其身份，并且  
  
-   您需要提供您自己的用户界面窗体作为某一网站上不同页之间的登录页。  
  
 在编写支持窗体身份验证的自定义安全扩展插件时，应注意以下事项：  
  
-   如果您使用窗体身份验证，则必须在 Internet 信息服务 (IIS) 的报表服务器虚拟目录上启用匿名访问。  
  
-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 身份验证必须设置为“窗体”。 在报表服务器的 Web.config 文件中配置 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 身份验证。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 在验证用户的身份并为其授权时，既可以使用 Windows 身份验证，也可以使用自定义身份验证，但不能同时使用二者。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 不支持同时使用多个安全扩展插件。  
  
## <a name="see-also"></a>另请参阅  
 [实现安全扩展插件](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
  
  
