---
title: 将 RenderedOutputFile 类用于传递扩展插件 | Microsoft Docs
description: 了解传递扩展插件如何使用 RenderedOutputFile 类，该类存储呈现的报表或报表资源。
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f743227a2927ad97c5a0bcc76c3634726969caef
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529103"
---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>将 RenderedOutputFile 类用于传递扩展插件
  <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 类表示某个数据流以及有关该数据流的关联属性的信息。 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 类的 Data 属性用于将呈现的报表或报表资源表示为 Stream 对象 。  
  
 Report 对象的 <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> 方法返回包含一个或多个 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象的数组，这些对象一起构成单个呈现的报表。 第一个 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象为呈现的报表。 任何其他 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象为必须随报表数据一起传递的资源（例如，HTML 文件和关联的图像）。 属于单一流呈现扩展插件（IMAGE、PDF、MHTML 和 EXCEL）的呈现扩展插件只返回此数组中的一个 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象。  
  
 有关如何使用 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 类的示例，请参阅 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="see-also"></a>另请参阅  
 [实现传递扩展插件](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
