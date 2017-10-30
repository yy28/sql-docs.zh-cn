---
title: "对数据处理扩展插件实施命令类 |Microsoft 文档"
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
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: b601aa43ecce5347f7229999455360be761f3bd3
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>为数据处理扩展插件实现 Command 类
  **命令**对象发出请求，并将其传递到数据源。 命令文本可以采用多种不同的语法形式，包括文本和 XML。 如果返回结果，**命令**对象返回的结果与**DataReader**对象。  
  
 若要创建**命令**类中，实现<xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>。 实现<xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>方法以返回结果设置为**DataReader**对象。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>方法你**命令**类应包含一个实现，采用<xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior>作为自变量的枚举。 如果您将数据处理扩展插件部署到报表设计器，则提供在 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> 方法中处理 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 事例的实现。 仅架构实现用于向报表设计器提供字段列表。 **DataReader**返回对象<xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>方法需要包含的字段，类型和名称信息或列，在你的结果集中。  
  
 （可选） 你**命令**类可以实现<xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。 这一接口使实现类可以分析某一查询并返回该查询中参数的列表。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 接口的这一功能仅用于报表设计器中。 实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 后，只要某一报表在预览模式下运行，就可以提示报表设计器的用户输入参数。 此外，你可以查看中的参数**参数**选项卡**数据集**对话框。  
  
> [!NOTE]  
>  如果您的自定义数据处理扩展插件不支持参数，则不应实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。  
  
 有关示例**命令**类实现，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

