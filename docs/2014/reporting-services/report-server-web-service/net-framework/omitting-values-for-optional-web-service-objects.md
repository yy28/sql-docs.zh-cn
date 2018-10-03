---
title: 省略可选 Web 服务对象的值 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8ce8a1662a57a4273e6449ecb94a410cd4dd798f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192807"
---
# <a name="omitting-values-for-optional-web-service-objects"></a>省略可选 Web 服务对象的值
  多个报表服务器 Web 服务复杂类型的属性具有名为“Specified”属性的伴随属性。 该属性的名称由原始属性名称再加上“Specified”构成。 具有此属性则指示原始属性的值有时可以省略。 这是从 Web 服务描述语言 (WSDL) 转换到 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 代理类的直接结果。 例如，复杂类型 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 的 Web 服务属性 <xref:ReportService2010.DataSourceDefinition> 具有名为 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 的伴随属性。 如果要生成应用程序而不想设置 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 属性的值，则不必提供 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 的值；此时将使用 `true` 的默认值。 但是，仍然需要将 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 设置为 `false`。 如果提供了 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 属性的值，则需要将 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 设置为等于 `true`。 这是对可写属性而言的。 对于只读属性，不需要执行任何操作。  
  
> [!IMPORTANT]  
>  未能使用上述方法指定属性可能会导致不可预知的 Web 服务行为。  
  
 通常要求您处理附加指定属性的数据类型是`Boolean`， `DateTime`，和`Enumeration`。  
  
 有关示例，请参阅 <xref:ReportService2010.ReportingService2010.CreateDataSource%2A> 方法。  
  
## <a name="see-also"></a>请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](building-applications-using-the-web-service-and-the-net-framework.md)   
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)  
  
  
