---
title: 调用 Web 服务方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Web service [Reporting Services], calls
- calling Web service
- Report Server Web service, SOAP
- XML Web service [Reporting Services], calls
- Report Server Web service, calls
- XML Web service [Reporting Services], SOAP
- SOAP [Reporting Services], calls
ms.assetid: f6f0c6e3-8bb5-4c44-9d19-1872edc72746
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3930eb35a5e145b44accc099087a41239b06a4b0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026108"
---
# <a name="calling-web-service-methods"></a>调用 Web 服务方法
  当使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 代理类调用 Web 服务操作时，可以通过使用该类的方法来实现。 这些方法的响应方式类似于 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 类库中类的任何其他方法。 所有 Web 服务方法都具有公共访问，并要求您提供适当数量的参数和参数类型。 在项目中创建代理类的实例之后，您可以调用方法以通过报表服务器执行报表操作。 以下 C# 代码说明如何使用 <xref:ReportService2010.ReportingService2010> 代理类的 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 方法。 此代码用于对返回 <xref:ReportService2010.CatalogItem> 对象数组（此数组包含报表服务器数据库中所有项的列表）的 Web 服务进行递归调用：  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
Dim items As CatalogItem() = rs.ListChildren("/", True)  
```  
  
```csharp  
ReportingService2010 rs = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
CatalogItem[] items = rs.ListChildren("/", true);  
```  
  
## <a name="see-also"></a>请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../report-server-web-service.md)   
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)  
  
  
