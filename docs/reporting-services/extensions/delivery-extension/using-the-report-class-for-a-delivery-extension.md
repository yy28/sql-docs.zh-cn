---
title: "将 Report 类用于传递扩展插件 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], report information
- Report class
ms.assetid: 1145ac63-eafd-452a-82af-16f85b1676dd
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f74c4848721333e0cebb1d7292c28646b3f07fe7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="using-the-report-class-for-a-delivery-extension"></a>将 Report 类用于传递扩展插件
  <xref:Microsoft.ReportingServices.Interfaces.Report> 类表示报表服务器数据库中的报表。 任何订阅都与某一特定报表相关联。 该报表包含在通知中。 您的传递扩展插件可以使用作为该通知的一部分的 <xref:Microsoft.ReportingServices.Interfaces.Report> 对象来呈现报表。 <xref:Microsoft.ReportingServices.Interfaces.Report> 对象还包含特定于报表的属性，例如指向报表服务器上的报表的 URL 和报表名称。 这些属性全都可以用作您的传递提供程序的一部分。  
  
 <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> 类的 <xref:Microsoft.ReportingServices.Interfaces.Report> 方法可用于呈现一个报表。 <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> 方法返回包含一个或多个 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象的数组，这些对象一起构成单个所呈现报表。 第一个 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象为呈现的报表。 任何其他 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象为必须随报表数据一起传递的资源（例如，HTML 文件和关联的图像）。 属于单一流呈现扩展插件（IMAGE、PDF、MHTML 和 Excel）的呈现扩展插件只返回此数组中的一个 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象。  
  
 包含报表流的 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象可作为传递的一部分。  
  
 有关如何使用 <xref:Microsoft.ReportingServices.Interfaces.Report> 类的示例，请参阅 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）  
  
## <a name="see-also"></a>另请参阅  
 [实现传递扩展插件](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)   
 [将 RenderedOutputFile 类用于传递扩展插件](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
  
  
