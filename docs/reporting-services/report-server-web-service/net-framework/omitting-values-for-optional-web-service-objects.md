---
title: 省略可选 Web 服务对象的值 | Microsoft Docs
description: 报表服务器 Web 服务复杂类型的某些属性支持 Specified 属性，因此你可以省略某些可写属性的值。
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3a7ea9c535092201eaa2c901ef11975bf1461d52
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "79509668"
---
# <a name="omitting-values-for-optional-web-service-objects"></a>省略可选 Web 服务对象的值
  多个报表服务器 Web 服务复杂类型的属性具有名为“Specified”属性的伴随属性。 该属性的名称由原始属性名称再加上“Specified”构成。 具有此属性则指示原始属性的值有时可以省略。 这是从 Web 服务描述语言 (WSDL) 转换到 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 代理类的直接结果。 例如，复杂类型 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 的 Web 服务属性 <xref:ReportService2010.DataSourceDefinition> 具有名为 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 的伴随属性。 如果要生成应用程序而不想设置 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 属性的值，则不必提供 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 的值；此时使用默认值 true  。 但是，仍需将 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 设置为 false  。 如果提供了 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 属性的值，则需要将 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 设置为等于 true  。 这是对可写属性而言的。 对于只读属性，不需要执行任何操作。  
  
> [!IMPORTANT]  
>  未能使用上述方法指定属性可能会导致不可预知的 Web 服务行为。  
  
 通常要求处理附加“Specified”属性的数据类型是 Boolean、DateTime 和 Enumeration    。  
  
 有关示例，请参阅 <xref:ReportService2010.ReportingService2010.CreateDataSource%2A> 方法。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [技术参考 (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
