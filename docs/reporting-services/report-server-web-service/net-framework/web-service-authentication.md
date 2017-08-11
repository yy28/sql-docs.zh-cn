---
title: "Web 服务身份验证 |Microsoft 文档"
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
- Web service [Reporting Services], authentication
- XML Web service [Reporting Services], authentication
- Report Server Web service, authentication
ms.assetid: 852b4947-a090-4e54-8555-5a503945ceab
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: be7e76aa26ca4b94afd2e32b40b9fbfbe92b170d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="web-service-authentication"></a>Web 服务身份验证
  可以使用 Windows 身份验证或基本身份验证对针对报表服务器 Web 服务进行的调用进行身份验证。 对报表服务器发出 SOAP 请求的任何客户端都必须实现其中一种支持的身份验证协议的客户端部分。 如果你使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]，你可以使用托管的代码 HTTP 类来实现身份验证。 通过使用这些 API，可以轻松地随 SOAP 请求一起发送身份验证信息。  
  
 如果在对报表服务器 Web 服务进行调用之前不具备适当的凭据，则调用将失败。 在运行时，你可以将凭据传递给 Web 服务通过设置**凭据**之前调用其方法表示 Web 服务的客户端对象的属性。  
  
 以下各节包含使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 发送凭据的示例代码。  
  
## <a name="windows-authentication"></a>Windows 身份验证  
 以下代码将 Windows 凭据传递到 Web 服务。  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
ReportingService rs = new ReportingService();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
```  
  
## <a name="basic-authentication"></a>基本身份验证  
 以下代码将基本身份验证凭据传递到 Web 服务。  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = New System.Net.NetworkCredential("username", "password", "domain")  
```  
  
```csharp  
ReportingService service = new ReportingService();  
service.Credentials = new System.Net.NetworkCredential("username", "password", "domain");  
```  
  
 必须在调用报表服务器 Web 服务的任何方法之前设置凭据。 如果您没有设置凭据，将收到错误代码“HTTP 401 错误: 拒绝访问”。 使用它，但设置凭据之后，你不需要再次设置它们，只要你继续使用相同的服务变量之前，必须验证服务 (如*rs*)。  
  
## <a name="custom-authentication"></a>自定义身份验证  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包含一个编程 API，它向开发人员提供了设计和开发自定义身份验证扩展插件（称为安全扩展插件）的机会。 有关详细信息，请参阅 [Implementing a Security Extension](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和.NET Framework 构建应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
