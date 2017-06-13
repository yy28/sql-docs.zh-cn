---
title: "提供 Web 服务方法参数 |Microsoft 文档"
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
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
caps.latest.revision: 38
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 43fcfe6eecffdc237366eb7963a5582b1915d363
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="supplying-web-service-method-arguments"></a>提供 Web 服务方法参数
  报表服务器 Web 服务方法通过 HTTP 上的 SOAP 向位于指定 URL 处的服务发送请求。 此服务接收请求，对其进行处理，然后返回响应。 这些请求和响应采用 XML 文档形式。  
  
## <a name="optional-parameters"></a>可选参数  
 在某些情况下，Web 服务方法可能具有可选输入参数。 即使 Web 服务方法的输入的参数是可选的仍必须将其包括并将参数值设置为**null** (**执行任何操作**中[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)])。 将参数值设置为**null**将 SOAP 请求中设置该参数的元素值**null**。  
  
 以下示例使用 <xref:ReportService2010.ReportingService2010.CreateFolder%2A> 方法在 Sales 文件夹中创建名为 Product Sales 的新文件夹。 通过提供**null**为文件夹提供文件夹属性中，没有特定于用户的属性的值是：  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>复杂数据类型  
 报表服务器 Web 服务的核心类为 <xref:ReportService2010.ReportingService2010>，您可以使用它调用 SOAP 操作或代理类的 Web 方法。 为了支持该类及其方法，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包含用户定义的、特定于 Web 服务方法的输入和输出参数的复杂数据类型。 这些复杂的数据类型是生成的代理类，你可以使用在开发时的一部分[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]环境。  
  
 当您生成代理类时，在 WSDL 文件中定义的复杂数据类型将由该代理的各个类表示，这些类包含与复杂数据类型的各种 SOAP 元素相对应的属性。 这些数据类型的序列成为由您在代码中可以枚举的对象组成的数组。 这样，就不再需要直接使用在 SOAP 消息中发送的 XML 结构。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 将为您处理该转换。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和.NET Framework 构建应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技术参考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
