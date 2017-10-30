---
title: "使用适用于的传递扩展插件 RenderedOutputFile 类 |Microsoft 文档"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 35fa7b98c43bb20ef6df30f27ca74a5f2ada1792
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>将 RenderedOutputFile 类用于传递扩展插件
  <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 类表示某个数据流以及有关该数据流的关联属性的信息。 **数据**属性<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>类用于表示呈现的报表或报表资源作为**流**对象。  
  
 <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A>方法**报表**对象返回的一个或多个数组<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>一起构成单个呈现的报表的对象。 第一个 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象为呈现的报表。 任何其他 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象为必须随报表数据一起传递的资源（例如，HTML 文件和关联的图像）。 属于单一流呈现扩展插件（IMAGE、PDF、MHTML 和 EXCEL）的呈现扩展插件只返回此数组中的一个 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 对象。  
  
 有关如何使用的示例<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>类，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

