---
title: "日志记录和在数据中定义日志项流组件 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- logs [Integration Services], custom
- custom log entries [Integration Services]
- custom data flow components [Integration Services], logging
- data flow components [Integration Services], logging
ms.assetid: 2190dba9-59b5-480b-b8e9-21d5a54c5917
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a0cbdbb818c7299221172f5ceb9b4ee5c54bddcb
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="logging-and-defining-log-entries-in-a-data-flow-component"></a>在数据流组件中记录和定义日志条目
  自定义数据流组件可使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.PostLogMessage%2A> 接口的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法将消息发布到现有日志条目。 还可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A> 方法或者 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 接口的类似方法向用户显示信息。 但是，此方法会导致引发和处理额外事件的开销，并且迫使用户从冗长的信息性消息中筛选出感兴趣的消息。 可以按如下所述使用自定义日志条目，为组件的用户提供不同标记的自定义日志信息。  
  
## <a name="registering-and-using-a-custom-log-entry"></a>注册和使用自定义日志条目  
  
### <a name="registering-a-custom-log-entry"></a>注册自定义日志条目  
 若要注册组件使用的自定义日志条目，请重写 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterLogEntries%2A> 基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。 下面的示例注册自定义日志条目并提供名称和说明。  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime;  
...  
private const string MyLogEntryName = "My Custom Component Log Entry";  
private const string MyLogEntryDescription = "Log entry from My Custom Component ";  
...  
    public override void RegisterLogEntries()  
    {  
      this.LogEntryInfos.Add(MyLogEntryName,  
        MyLogEntryDescription,  
        Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT);  
    }  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
...  
Private Const MyLogEntryName As String = "My Custom Component Log Entry"   
Private Const MyLogEntryDescription As String = "Log entry from My Custom Component "  
...  
Public  Overrides Sub RegisterLogEntries()   
  Me.LogEntryInfos.Add(MyLogEntryName, _  
    MyLogEntryDescription, _  
    Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT)   
End Sub  
```  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency> 枚举向运行时提示记录事件将采用的频率：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_OCCASIONAL>：只是有时候记录事件，不是每次执行都记录。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>：每次执行的过程中，记录事件一定的次数。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_PROPORTIONAL>：记录事件的次数与完成的工作量成比例。  
  
 上面的示例使用 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>，因为组件希望每执行一次记录一条。  
  
 注册自定义日志项并将自定义组件的实例添加到数据流设计器图面之后,**日志记录**设计器中的对话框中显示新的日志条目具有名称"我自定义组件日志条目"中的可用日志条目列表。  
  
### <a name="logging-to-a-custom-log-entry"></a>记录到自定义日志条目  
 注册完自定义日志条目后，组件即可记录自定义消息。 下面的示例在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 方法的执行过程中写入自定义日志条目，其中包含组件所使用的 SQL 语句文本。  
  
```csharp  
public override void PreExecute()  
{  
  DateTime now = DateTime.Now;  
  byte[] additionalData = null;  
  this.ComponentMetaData.PostLogMessage(MyLogEntryName,  
    this.ComponentMetaData.Name,  
    "Command Sent was: " + myCommand.CommandText,  
    now, now, 0, ref additionalData);  
}  
```  
  
```vb  
Public  Overrides Sub PreExecute()   
  Dim now As DateTime = DateTime.Now   
  Dim additionalData As Byte() = Nothing   
  Me.ComponentMetaData.PostLogMessage(MyLogEntryName, _  
    Me.ComponentMetaData.Name, _  
    "Command Sent was: " + myCommand.CommandText, _  
    now, now, 0, additionalData)   
End Sub  
```  
  
 现在当用户执行的包，选择"我自定义组件日志条目"后在**日志记录**对话框中，日志将包含清楚地标记为"User::My 自定义组件日志条目。"的条目 此新日志条目包含 SQL 语句文本、时间戳和开发人员记录的所有其他数据。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS &#41;日志记录](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

