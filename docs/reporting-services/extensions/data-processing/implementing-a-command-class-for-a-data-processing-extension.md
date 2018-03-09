---
title: "为数据处理扩展插件实现 Command 类 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
caps.latest.revision: "35"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9a27be96535c6ec9c27d19e8d3c803d7a97ca083
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>为数据处理扩展插件实现 Command 类
  Command 对象表述请求并将其传递到数据源上。 命令文本可以采用多种不同的语法形式，包括文本和 XML。 如果返回结果，则 Command 对象将结果作为 DataReader 对象返回。  
  
 若要创建某一 Command 类，请实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>。 实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法以便将结果集作为 DataReader 对象返回。 Command 类的 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法应包括采用 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> 枚举作为参数的实现。 如果您将数据处理扩展插件部署到报表设计器，则提供在 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> 方法中处理 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 事例的实现。 仅架构实现用于向报表设计器提供字段列表。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法返回的 DataReader 对象需要为结果集中的字段（或列）包含类型和名称信息。  
  
 或者，也可以使用 Command 类来实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。 这一接口使实现类可以分析某一查询并返回该查询中参数的列表。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 接口的这一功能仅用于报表设计器中。 实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 后，只要某一报表在预览模式下运行，就可以提示报表设计器的用户输入参数。 此外，可以在“数据集”对话框的“参数”选项卡中查看这些参数。  
  
> [!NOTE]  
>  如果您的自定义数据处理扩展插件不支持参数，则不应实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。  
  
 有关 Command 类实现的示例，请参阅 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
