---
title: "以编程方式处理事件 |Microsoft 文档"
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
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services packages, events
- SQL Server Integration Services packages, events
- SSIS events, programmatically handling
- packages [Integration Services], events
- DtsEventHandler object
- SSIS packages, events
- SSIS events
- events [Integration Services], programmatically
- tasks [Integration Services], events
- IDTSEvents interface
ms.assetid: 0f00bd66-efd5-4f12-9e1c-36195f739332
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 7235703f494bd1fb50e696aef537391ba23d1749
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="handling-events-programmatically"></a>以编程方式处理事件
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 运行时提供了一个事件集合，该集合中的事件在包的验证和执行过程之前、期间和之后发生。 这些事件可用两种方法捕获。 第一种方法是通过实现<xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>接口在类中，并作为参数传递给提供类**执行**和**验证**的包的方法。 第二种方法是创建 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 对象，该对象可以包含当 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 中的事件发生时所执行的其他 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 对象，例如任务和循环。 本节介绍这两种方法并提供代码示例来说明它们的用法。  
  
## <a name="receiving-idtsevents-callbacks"></a>接收 IDTSEvents 回调  
 以编程方式生成和执行包的开发人员可以使用 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 接口在验证和执行过程中接收事件通知。 这可通过创建一个类以实现<xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>接口和作为参数传递给提供此类**验证**和**执行**的包的方法。 运行时引擎随后会在事件发生时调用该类的这些方法。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> 类是一个已实现 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 接口的类；因此，直接实现 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 的另一种方法是从 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> 继承并重写要响应的特定事件。 然后作为参数传递给提供你的类**验证**和**执行**方法<xref:Microsoft.SqlServer.Dts.Runtime.Package>以接收事件回调。  
  
 以下代码示例演示从 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> 继承的类，并重写 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnPreExecute%2A> 方法。 然后提供此类可作为 aparameter 到**验证**和**执行**的包的方法。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      MyEventsClass eventsClass = new MyEventsClass();  
  
      p.Validate(null, null, eventsClass, null);  
      p.Execute(null, null, eventsClass, null, null);  
  
      Console.Read();  
    }  
  }  
  class MyEventsClass : DefaultEvents  
  {  
    public override void OnPreExecute(Executable exec, ref bool fireAgain)  
    {  
      // TODO: Add custom code to handle the event.  
      Console.WriteLine("The PreExecute event of the " +  
        exec.ToString() + " has been raised.");  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim eventsClass As MyEventsClass = New MyEventsClass()  
  
    p.Validate(Nothing, Nothing, eventsClass, Nothing)  
    p.Execute(Nothing, Nothing, eventsClass, Nothing, Nothing)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
Class MyEventsClass  
  Inherits DefaultEvents  
  
  Public Overrides Sub OnPreExecute(ByVal exec As Executable, ByRef fireAgain As Boolean)  
  
    ' TODO: Add custom code to handle the event.  
    Console.WriteLine("The PreExecute event of the " & _  
      exec.ToString() & " has been raised.")  
  
  End Sub  
  
End Class  
```  
  
## <a name="creating-dtseventhandler-objects"></a>创建 DtsEventHandler 对象  
 运行时引擎通过 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 对象提供一个高度灵活而可靠的事件处理和通知系统。 可以使用这些对象在事件处理程序中设计整个工作流，而这些工作流只在该事件处理程序所属的事件发生时才执行。 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 对象是一个容器，该容器在其父对象上的相应事件激发时执行。 此体系结构使您可以创建为响应容器上发生的事件而执行的孤立工作流。 由于 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 对象是同步的，因此在附加到事件的事件处理程序返回之前，执行过程不会继续。  
  
 下面的代码演示如何创建 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 对象。 该代码将 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> 添加到包的 <xref:Microsoft.SqlServer.Dts.Runtime.Package.Executables%2A> 集合，然后为该任务的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 事件创建一个 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> 对象。 该事件处理程序中添加了一个 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>，该处理程序在第一个 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> 发生 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> 事件时执行。 此示例假定存在一个用于测试的名为 C:\Windows\Temp\DemoFile.txt 的文件。 第一次运行该示例时，它会成功复制该文件，并且不会调用事件处理程序。 第二次运行此示例中，第一个<xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>将文件复制失败 (因为的值<xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask.OverwriteDestinationFile%2A>是**false**)，调用事件处理程序时，第二个<xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>由于发生的错误中删除源文件和包报告失败。  
  
## <a name="example"></a>示例  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string f = "DemoFile.txt";  
      Executable e;  
      TaskHost th;  
      FileSystemTask fst;  
  
      Package p = new Package();  
  
      p.Variables.Add("sourceFile", true, String.Empty,  
        @"C:\Windows\Temp\" + f);  
      p.Variables.Add("destinationFile", true, String.Empty,  
        Path.Combine(Directory.GetCurrentDirectory(), f));  
  
      // Create a first File System task and add it to the package.  
      // This task tries to copy a file from one folder to another.  
      e = p.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask1";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.CopyFile;  
      fst.OverwriteDestinationFile = false;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
      fst.Destination = "destinationFile";  
      fst.IsDestinationPathVariable = true;  
  
      // Add an event handler for the FileSystemTask's OnError event.  
      DtsEventHandler ehOnError = (DtsEventHandler)th.EventHandlers.Add("OnError");  
  
      // Create a second File System task and add it to the event handler.  
      // This task deletes the source file if the event handler is called.  
      e = ehOnError.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask2";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.DeleteFile;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
  
      DTSExecResult vr = p.Validate(null, null, null, null);  
      Console.WriteLine("ValidationResult = " + vr.ToString());  
      if (vr == DTSExecResult.Success)  
      {  
        DTSExecResult er = p.Execute(null, null, null, null, null);  
        Console.WriteLine("ExecutionResult = " + er.ToString());  
        if (er == DTSExecResult.Failure)  
          if (!File.Exists(@"C:\Windows\Temp\" + f))  
            Console.WriteLine("Source file has been deleted by the event handler.");  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim f As String = "DemoFile.txt"  
    Dim e As Executable  
    Dim th As TaskHost  
    Dim fst As FileSystemTask  
  
    Dim p As Package = New Package()  
  
    p.Variables.Add("sourceFile", True, String.Empty, _  
      "C:\Windows\Temp\" & f)  
    p.Variables.Add("destinationFile", True, String.Empty, _  
      Path.Combine(Directory.GetCurrentDirectory(), f))  
  
    ' Create a first File System task and add it to the package.  
    ' This task tries to copy a file from one folder to another.  
    e = p.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.CopyFile  
    fst.OverwriteDestinationFile = False  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
    fst.Destination = "destinationFile"  
    fst.IsDestinationPathVariable = True  
  
    ' Add an event handler for the FileSystemTask's OnError event.  
    Dim ehOnError As DtsEventHandler = CType(th.EventHandlers.Add("OnError"), DtsEventHandler)  
  
    ' Create a second File System task and add it to the event handler.  
    ' This task deletes the source file if the event handler is called.  
    e = ehOnError.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.DeleteFile  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
  
    Dim vr As DTSExecResult = p.Validate(Nothing, Nothing, Nothing, Nothing)  
    Console.WriteLine("ValidationResult = " + vr.ToString())  
    If vr = DTSExecResult.Success Then  
      Dim er As DTSExecResult = p.Execute(Nothing, Nothing, Nothing, Nothing, Nothing)  
      Console.WriteLine("ExecutionResult = " + er.ToString())  
      If er = DTSExecResult.Failure Then  
        If Not File.Exists("C:\Windows\Temp\" + f) Then  
          Console.WriteLine("Source file has been deleted by the event handler.")  
        End If  
      End If  
    End If  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS &#41;事件处理程序](../../integration-services/integration-services-ssis-event-handlers.md)   
 [将事件处理程序添加到包](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  

