---
title: "引发并在数据中定义的事件流组件 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow components [Integration Services], events
- events [Integration Services], custom
- custom events [Integration Services]
- custom data flow components [Integration Services], events
- events [Integration Services], raising
- predefined events [Integration Services]
ms.assetid: 1d8c5358-9384-47a8-b7cb-7b0650384119
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a900b27c9056d95fb2284d8ba9d6b09d9c6635b5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="raising-and-defining-events-in-a-data-flow-component"></a>在数据流组件中引发和定义事件
  组件开发人员可通过调用对 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 属性公开的方法，引发在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 接口中定义的一部分事件。 还可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> 集合定义自定义事件，并使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 方法在执行过程中引发这些事件。 本节介绍如何创建和引发事件，并提供在设计时应于何时引发事件的指南。  
  
## <a name="raising-events"></a>引发事件  
 组件通过引发事件**激发\<X >**方法<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>接口。 您可以在组件设计和执行的过程中引发事件。 通常，在组件设计过程中，验证期间会调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A> 方法。 这些事件显示中的消息**错误列表**窗格[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]和时组件的配置不正确，向该组件的用户提供反馈。  
  
 组件也可以在执行过程中的任一点引发事件。 组件开发人员可通过事件在组件执行时向该组件的用户提供反馈。 在执行过程中调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> 方法可能导致包失败。  
  
## <a name="defining-and-raising-custom-events"></a>定义和引发自定义事件  
  
### <a name="defining-a-custom-event"></a>定义自定义事件  
 调用 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> 集合的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> 方法可创建自定义事件。 此集合由数据流任务设置，并作为属性通过 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基类提供给组件开发人员。 此类包含调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 方法的过程中由数据流任务定义的自定义事件和组件定义的自定义事件。  
  
 组件的自定义事件不会持久保留在包 XML 中。 因此，在设计和执行过程中都调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 方法，以允许组件定义所引发的事件。  
  
 *此*参数<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A>方法指定组件是否允许<xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>事件创建的对象。 请注意，<xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> 是同步的。 因此，直到附加到自定义事件的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 执行完毕后，组件才会继续执行。 如果*此*参数是**true**，每个参数的事件自动将提供给任何<xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>对象通过创建并自动填充变量[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]运行时。  
  
### <a name="raising-a-custom-event"></a>引发自定义事件  
 通过调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 方法并提供事件的名称、文本和参数，组件可引发自定义事件。 如果*此*参数是**true**、 任何<xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers>，创建用于自定义事件由执行[!INCLUDE[ssIS](../../../includes/ssis-md.md)]运行时引擎。  
  
### <a name="custom-event-sample"></a>自定义事件示例  
 下面的代码示例演示了在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 方法中定义自定义事件，然后通过调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 方法在运行时引发该事件的组件。  
  
```csharp  
public override void RegisterEvents()  
{  
    string [] parameterNames = new string[2]{"RowCount", "StartTime"};  
    ushort [] parameterTypes = new ushort[2]{ DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)};  
    string [] parameterDescriptions = new string[2]{"The number of rows to sort.", "The start time of the Sort operation."};  
    EventInfos.Add("StartingSort","Fires when the component begins sorting the rows.",false,ref parameterNames, ref paramterTypes, ref parameterDescriptions);  
}  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
    while (buffer.NextRow())  
    {  
       // Process buffer rows.  
    }  
  
    IDTSEventInfo100 eventInfo = EventInfos["StartingSort"];  
    object []arguments = new object[2]{buffer.RowCount, DateTime.Now };  
    ComponentMetaData.FireCustomEvent("StartingSort", "Beginning sort operation.", ref arguments, ComponentMetaData.Name, ref FireSortEventAgain);  
}  
```  
  
```vb  
Public  Overrides Sub RegisterEvents()   
  Dim parameterNames As String() = New String(2) {"RowCount", "StartTime"}   
  Dim parameterTypes As System.UInt16() = New System.UInt16(2) {DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)}   
  Dim parameterDescriptions As String() = New String(2) {"The number of rows to sort.", "The start time of the Sort operation."}   
  EventInfos.Add("StartingSort", "Fires when the component begins sorting the rows.", False, parameterNames, paramterTypes, parameterDescriptions)   
End Sub   
  
Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
  While buffer.NextRow   
  End While   
  Dim eventInfo As IDTSEventInfo100 = EventInfos("StartingSort")   
  Dim arguments As Object() = New Object(2) {buffer.RowCount, DateTime.Now}   
  ComponentMetaData.FireCustomEvent("StartingSort", _  
    "Beginning sort operation.", arguments, _  
    ComponentMetaData.Name, FireSortEventAgain)   
End Sub  
```  

## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS &#41;事件处理程序](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [将事件处理程序添加到包](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  

