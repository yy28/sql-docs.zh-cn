---
title: Reporting Services 中的授权 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- authorization [Reporting Services]
ms.assetid: 15fc1c7b-560c-4737-b126-e0d428a1b530
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5141ca13693d140e56700b46e030e1eb2b14e0e0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026998"
---
# <a name="authorization-in-reporting-services"></a>Reporting Services 中的授权
  授权是指确定是否应为某个身份授予其请求的、针对报表服务器数据库的给定资源的访问权限的过程。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 使用基于角色的授权体系结构，根据用户的应用程序角色分配为用户授予针对给定资源的访问权限。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的安全扩展插件包含对一个授权组件的实现，该组件用于在报表服务器上对用户进行身份验证后授予用户访问权限。 在某一用户尝试通过 SOAP API 和通过 URL 访问对系统或报表服务器项执行操作时，调用授权。 这可通过安全扩展插件接口**IAuthorizationExtension**。 如前所述，所有扩展插件均继承自 IExtension，这是部署的所有扩展插件的基接口。 **IExtension**并**IAuthorizationExtension**属于**Microsoft.ReportingServices.Interfaces**命名空间。  
  
## <a name="checking-access"></a>检查访问  
 在授权中，任何自定义安全实现的关键环节都是访问权限检查，访问权限检查是在 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 方法中实现的。 每当用户尝试对报表服务器执行操作时，就会调用 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>。 为每个操作类型都将重载 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 方法。 对于文件夹操作，访问检查的示例可能如下：  
  
```  
// Overload for Folder operations  
public bool CheckAccess(  
   string userName,   
   IntPtr userToken,   
   byte[] secDesc,   
   FolderOperation requiredOperation)  
{  
   // If the user is the administrator, allow unrestricted access.  
   if (userName == m_adminUserName)   
      return true;  
  
   AceCollection acl = DeserializeAcl(secDesc);  
   foreach(AceStruct ace in acl)  
   {  
         if (userName == ace.PrincipalName)  
         {  
            foreach(FolderOperation aclOperation in   
               ace.FolderOperations)  
            {  
               if (aclOperation == requiredOperation)  
                     return true;  
            }  
         }  
   }  
   return false;  
}  
```  
  
 通过传入登录用户的名称、用户标记、项的安全描述符和请求的操作，报表服务器调用 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 方法。 在此处，您将检查用户名的安全描述符和相应权限以完成该请求，然后返回 `true` 以指示授予访问，或者返回 `false` 以指示拒绝访问。  
  
## <a name="security-descriptors"></a>安全描述符  
 在设置针对报表服务器数据库中的项的授权策略时，客户端应用程序（例如报表管理器）会将用户信息提交到安全扩展插件，同时提交用于该项的安全策略。 此安全策略和用户信息统称为安全描述符。 安全描述符包含报表服务器数据库中某一项的以下信息：  
  
-   具有对项执行操作所需的某一类型权限的组或用户。  
  
-   项的类型。  
  
-   控制对项的访问的任意访问控制列表。  
  
 安全描述符是使用 Web 服务 <xref:ReportService2010.ReportingService2010.SetPolicies%2A> 和 <xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A> 方法创建的。  
  
### <a name="authorization-flow"></a>授权流程  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 授权由当前配置为在服务器上运行的安全扩展插件控制。 授权是基于角色的，并且限制为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安全体系结构提供的权限和操作。 下图描述授权用户对报表服务器数据库中的项执行操作的流程：  
  
 ![Reporting Services 安全授权流程](../../media/rosettasecurityextensionauthorizationflow.gif "Reporting Services 安全授权流程")  
  
 如此图中所示，授权采用以下顺序：  
  
1.  一旦进行身份验证后，客户端应用程序通过 Reporting Services Web 服务方法对报表服务器进行请求。 身份验证票证将在每个 Web 请求的 HTTP 标头中以 cookie 的形式传递到报表服务器中。  
  
2.  将在任何访问检查前验证该 cookie。  
  
3.  一旦对 cookie 进行验证后，报表服务器将调用 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> 并且向用户授予某一身份。  
  
4.  用户尝试通过 Reporting Services Web 服务执行某一操作。  
  
5.  报表服务器调用 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 方法。  
  
6.  安全描述符被检索并传递到 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 的自定义安全扩展插件实现中。 此时，用户、组或计算机将与要访问的项的安全描述符进行比较，然后授权它们执行请求的操作。  
  
7.  如果已对用户授权，则 Web 服务将执行请求的操作并向调用应用程序返回响应。  
  
  
