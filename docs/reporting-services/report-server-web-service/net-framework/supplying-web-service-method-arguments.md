---
title: 提供 Web 服务方法参数 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a273ce7fb8ddcb53545c4fe95db8e6062a1e5b45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025404"
---
# <a name="supplying-web-service-method-arguments"></a>提供 Web 服务方法参数
  报表服务器 Web 服务方法通过 HTTP 上的 SOAP 向位于指定 URL 处的服务发送请求。 此服务接收请求，对其进行处理，然后返回响应。 这些请求和响应采用 XML 文档形式。  
  
## <a name="optional-parameters"></a>可选参数  
 在某些情况下，Web 服务方法可能具有可选输入参数。 即使 Web 服务方法的某个输入参数为可选，也仍必须包含该参数并将参数值设置为 null（在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中为“Nothing”）。 将参数值设置为 null 后，可将 SOAP 请求中该参数的元素值设置为 null。  
  
 以下示例使用 <xref:ReportService2010.ReportingService2010.CreateFolder%2A> 方法在 Sales 文件夹中创建名为 Product Sales 的新文件夹。 通过为文件夹属性提供 null 值，将不会为该文件夹提供用户特定的属性：  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>复杂数据类型  
 报表服务器 Web 服务的核心类为 <xref:ReportService2010.ReportingService2010>，您可以使用它调用 SOAP 操作或代理类的 Web 方法。 为了支持该类及其方法，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包含用户定义的、特定于 Web 服务方法的输入和输出参数的复杂数据类型。 这些复杂数据类型是所生成的代理类的一部分，当你在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 环境中进行开发时可以使用它们。  
  
 当您生成代理类时，在 WSDL 文件中定义的复杂数据类型将由该代理的各个类表示，这些类包含与复杂数据类型的各种 SOAP 元素相对应的属性。 这些数据类型的序列成为由您在代码中可以枚举的对象组成的数组。 这样，就不再需要直接使用在 SOAP 消息中发送的 XML 结构。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 将为您处理该转换。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技术参考 (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
