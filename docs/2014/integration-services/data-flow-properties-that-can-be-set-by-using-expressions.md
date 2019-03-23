---
title: 数据流可以通过使用表达式设置的属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, property expressions
- Integration Services packages, property expressions
- packages [Integration Services], properties
- SSIS packages, property expressions
- property expressions [Integration Services]
ms.assetid: cd0e171a-08be-45d6-81dc-ed94f37698b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2fd6b938d13e880f7ec8d48d3e4ca9665ee9cd65
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378595"
---
# <a name="data-flow-properties-that-can-be-set-by-using-expressions"></a>可以使用表达式设置的数据流属性
  可以使用数据流任务容器上的可用属性表达式来指定数据流对象的某些属性的值。  
  
 有关使用属性表达式的信息，请参阅 [在包中使用属性表达式](expressions/use-property-expressions-in-packages.md)。  
  
 可以使用属性表达式为包的每个已部署的实例自定义配置。 也可以使用属性表达式来为包指定运行时约束，方法是将 **/set** 选项与 **dtexec** 命令提示实用工具一起使用。 例如，可以约束排序转换使用的 `MaximumThreads`，或约束模糊分组和模糊查找转换的 `MaxMemoryUsage`。 如果无约束，则这些转换可能会在内存中高速缓存大量数据。  
  
 若要为本主题中列出的数据流对象的其中一个属性指定属性表达式，请在设计器的 **“控制流”** 图面上选择该数据流任务，或选择设计器的 **“数据流”** 选项卡但不选择任何单个组件或路径，以此方式显示数据流任务的 **“属性”** 窗口。 选择“表达式”属性，然后单击省略号 (...) 以显示“属性表达式编辑器”对话框。 下拉“属性”列表以选择某个属性，然后在“表达式”文本框中键入一个表达式，或者单击省略号 (...) 以显示“表达式生成器”对话框。  
  
 **“属性”** 列表仅显示那些已位于设计器的 **“数据流”** 图面上的数据流对象的可用属性。 因此，不能使用 **“属性”** 列表来查看那些支持属性表达式的数据流对象的所有可能的属性。 例如，如果已将 ADO NET 源放置在设计器图面，**属性**列表中包含的一项`[ADO NET Source].[SqlCommand]`属性。 该列表还显示了数据流任务自身的许多属性。  
  
## <a name="properties-of-data-flow-objects-that-support-property-expressions"></a>支持属性表达式的数据流对象的属性  
 下面的列表中的属性值可以使用属性表达式来指定。  
  
### <a name="data-flow-sources"></a>数据流源  
  
|数据流对象|“属性”|  
|----------------------|--------------|  
|ADO NET 源|TableOrViewName 属性<br /><br /> SqlCommand 属性|  
|XML 源|XMLData 属性<br /><br /> XMLSchemaDefinition 属性|  
  
### <a name="data-flow-transformations"></a>数据流转换  
 有关这些自定义属性的详细信息，请参阅 [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)。  
  
|数据流对象|属性|  
|----------------------|--------------|  
|有条件拆分转换|FriendlyExpression 属性|  
|派生列转换|FriendlyExpression 属性|  
|模糊分组转换|MaxMemoryUsage 属性|  
|模糊查找转换|MaxMemoryUsage 属性|  
|查找转换|SqlCommand 属性<br /><br /> SqlCommandParam 属性|  
|OLE DB 命令转换|SqlCommand 属性|  
|百分比抽样转换|SamplingValue 属性|  
|透视转换|PivotKeyValue 属性|  
|行抽样转换|SamplingValue 属性|  
|排序转换|MaximumThreads 属性|  
|逆透视转换|PivotKeyValue 属性|  
  
### <a name="data-flow-destinations"></a>数据流目标  
  
|数据流对象|属性|  
|----------------------|--------------|  
|ADO NET 目标|TableOrViewName 属性<br /><br /> BatchSize 属性<br /><br /> CommandTimeout 属性|  
|平面文件目标|Header 属性|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Compact 目标|TableName 属性|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]目标|BulkInsertTableName 属性<br /><br /> BulkInsertFirstRow 属性<br /><br /> BulkInsertLastRow 属性<br /><br /> BulkInsertOrder 属性<br /><br /> Timeout 属性|  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [添加或更改属性表达式](expressions/add-or-change-a-property-expression.md)  
  
## <a name="related-content"></a>相关内容  
 pragmaticworks.com 上的技术文章 [SSIS 表达式小抄表](http://pragmaticworks.com/cheatsheet/)。  
  
## <a name="see-also"></a>请参阅  
 [在包中使用属性表达式](expressions/use-property-expressions-in-packages.md)   
 [通用属性](../../2014/integration-services/common-properties.md)   
 [转换自定义属性](data-flow/transformations/transformation-custom-properties.md)   
 [路径属性](../../2014/integration-services/path-properties.md)  
  
  
