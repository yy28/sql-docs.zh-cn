---
title: "实现用于数据处理扩展插件的 DataReader 类 |Microsoft 文档"
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
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cfd3a6cb38c59b1810d046839cb3be4f0dc9846a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>为数据处理扩展插件实现 DataReader 类
  **DataReader**对象允许客户端从数据源检索数据的只读、 只进流。 查询执行以及存储在客户端上的网络缓冲区，直到你请求时，这些结果将返回使用**读取**方法**DataReader**类。 若要创建**DataReader**类中，实现<xref:Microsoft.ReportingServices.DataProcessing.IDataReader>并且可以选择实现<xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>。 使用**DataReader**对象提高应用程序性能这两个通过尽快它检索数据是可用，而不是整个在内存，从而减少系统开销中一次可返回，并且 （默认情况下） 存储的只有一个行的查询结果正在等待。  
  
 创建的实例之后你**命令**创建类， **DataReader**对象通过调用**Command.ExecuteReader**从数据源中检索行。 **DataReader**实现必须提供两个基本功能： 通过结果的只进访问设置获取通过执行命令并访问的列类型，名称，并在每个行值。 客户端使用**读取**方法**DataReader**对象从查询结果中获取行。  
  
 在报表设计器中，你**DataReader**对象用于检索字段，以及有关结果集的架构信息的列表。 这通过实现实现**GetName**， **GetValue**， **GetFieldType，**和**GetOrdinal**方法<xref:Microsoft.ReportingServices.DataProcessing.IDataReader>接口。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> 接口可用于提供与结果集有关的特定聚合信息。 有关示例**DataReader**类实现，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
