---
title: "省略可选的 Web 服务对象的值 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 3532a470bd036e0128a8df21ca391210cf7209a2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="omitting-values-for-optional-web-service-objects"></a>省略可选 Web 服务对象的值
  报表服务器 Web 服务的复杂类型的多个属性具有随附属性称为指定属性。 该属性的名称由原始属性名称再加上“Specified”构成。 具有此属性则指示原始属性的值有时可以省略。 这是从 Web 服务描述语言 (WSDL) 转换到 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 代理类的直接结果。 例如，复杂类型 <xref:ReportService2010.DataSourceDefinition.Enabled%2A> 的 Web 服务属性 <xref:ReportService2010.DataSourceDefinition> 具有名为 <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> 的伴随属性。 如果你正在生成的应用，并且不希望设置的值<xref:ReportService2010.DataSourceDefinition.Enabled%2A>属性，则不需要提供的值<xref:ReportService2010.DataSourceDefinition.Enabled%2A>; 默认值的**true**使用。 但是，仍需要设置<xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>到**false**。 如果提供的值<xref:ReportService2010.DataSourceDefinition.Enabled%2A>属性，你需要设置<xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>等于**true**。 这是对可写属性而言的。 对于只读属性，不需要执行任何操作。  
  
> [!IMPORTANT]  
>  未能使用上述方法指定属性可能会导致不可预知的 Web 服务行为。  
  
 通常需要处理其他的指定属性的数据类型是**布尔**， **DateTime**，和**枚举**。  
  
 有关示例，请参阅 <xref:ReportService2010.ReportingService2010.CreateDataSource%2A> 方法。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和.NET Framework 构建应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [技术参考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
