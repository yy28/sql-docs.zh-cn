---
title: 调用 Web 服务方法 | Microsoft Docs
description: 调用代理类的方法，以便对报表服务器执行报告操作。 Web 服务方法具有公共访问权限，并且需要适当的参数。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0e7347bfcb93d327bc6e56eb91c903bbc5e1f38f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "79198322"
---
# <a name="calling-web-service-methods"></a>调用 Web 服务方法
  当使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 代理类调用 Web 服务操作时，可以通过使用该类的方法来实现。 这些方法的响应方式类似于 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 类库中类的任何其他方法。 所有 Web 服务方法都具有公共访问，并要求您提供适当数量的参数和参数类型。 在项目中创建代理类的实例之后，您可以调用方法以通过报表服务器执行报表操作。 以下 C# 代码说明如何使用 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 代理类的 <xref:ReportService2010.ReportingService2010> 方法。 此代码用于对返回 <xref:ReportService2010.CatalogItem> 对象数组（此数组包含报表服务器数据库中所有项的列表）的 Web 服务进行递归调用：  
  
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
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技术参考 (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
