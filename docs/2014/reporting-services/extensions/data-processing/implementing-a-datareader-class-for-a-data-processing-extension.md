---
title: 为数据处理扩展插件实现 DataReader 类 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ff4ba3966523f05d9993df4af616048a16292ea4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091907"
---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>为数据处理扩展插件实现 DataReader 类
  DataReader 对象使客户端可以从数据源检索只读、只进的数据流。 结果作为查询执行返回，并且存储于客户端上的网络缓冲区中，直到使用 DataReader 类的读取方法请求它们。 要创建 DataReader 类，请实现 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader>，并可以选择实现 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>。 使用 DataReader 对象可以从多方面提高应用程序性能，包括可以在数据可用时立刻检索数据，而非等待返回整个查询结果，以及在内存中每次只存储一行（默认情况下），从而降低系统开销。  
  
 在创建 Command 类的某一实例后，通过调用 Command.ExecuteReader 创建一个 DataReader 对象，以便从数据源检索行。 DataReader 实现必须提供两个基本的功能：对通过执行某一命令获取的结果集进行只进访问，以及访问每一行内的列类型、名称和值。 客户端使用 DataReader 对象的读取方法从查询的结果获取某一行。  
  
 在报表设计器中，DataReader 对象用于检索字段列表以及与结果集有关的架构信息。 这是通过实现 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 接口的 GetName、GetValue、GetFieldType 和 GetOrdinal 方法实现的。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> 接口可用于提供与结果集有关的特定聚合信息。 有关示例 DataReader 类实现，请参阅 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 扩展插件](../reporting-services-extensions.md)   
 [实现数据处理扩展插件](implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
