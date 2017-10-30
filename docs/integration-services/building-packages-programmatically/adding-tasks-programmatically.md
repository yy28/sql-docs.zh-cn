---
title: "以编程方式添加任务 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- tasks [Integration Services], packages
- adding package tasks
ms.assetid: 5d4652d5-228c-4238-905c-346dd8503fdf
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 35fbfd1c17d88d684671050c297a19822b098479
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="adding-tasks-programmatically"></a>以编程方式添加任务
  可在运行时引擎中将任务添加到下列对象类型中：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Package>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Sequence>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>  
  
 这些类被视为容器，它们均继承了 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSequence.Executables%2A> 属性。 容器可包含任务集合，任务是在容器执行期间，由运行库处理的可执行对象。 集合中对象的执行顺序由对容器中每个任务设置的 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 确定。 使用优先约束可使执行基于集合中的 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 的成功、失败或完成进行分支跳转。  
  
 每个容器都有一个包含各个 <xref:Microsoft.SqlServer.Dts.Runtime.Executables> 对象的 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 集合。 每个可执行任务都继承并实现 <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Execute%2A> 方法和 <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Validate%2A> 方法。 运行时引擎会调用这两个方法来处理每个 <xref:Microsoft.SqlServer.Dts.Runtime.Executable>。  
  
 若要向包中添加任务，您需要一个具有现有 <xref:Microsoft.SqlServer.Dts.Runtime.Executables> 集合的容器。 大多数情况下，要添加到该集合中的任务为包。 若要添加新的任务可执行文件到该容器的集合，请调用<xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A>方法。 该方法只有一个参数，是个字符串，它包含要添加的任务的 CLSID、PROGID、STOCK 名字对象或 <xref:Microsoft.SqlServer.Dts.Runtime.TaskInfo.CreationName%2A>。  
  
## <a name="task-names"></a>任务名称  
 虽然可以指定一个任务，按名称或 ID， **STOCK**名字对象是中最经常使用的参数<xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A>方法。 若要将任务添加到可执行文件由标识**STOCK**标记时，使用以下语法：  
  
```csharp  
Executable exec = package.Executables.Add("STOCK:BulkInsertTask");  
  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add("STOCK:BulkInsertTask")  
  
```  
  
 以下列表显示之后使用的每个任务的名称**STOCK**名字对象。  
  
-   ActiveXScriptTask  
  
-   BulkInsertTask  
  
-   ExecuteProcessTask  
  
-   ExecutePackageTask  
  
-   Exec80PackageTask  
  
-   FileSystemTask  
  
-   FTPTask  
  
-   MSMQTask  
  
-   PipelineTask  
  
-   ScriptTask  
  
-   SendMailTask  
  
-   SQLTask  
  
-   TransferStoredProceduresTask  
  
-   TransferLoginsTask  
  
-   TransferErrorMessagesTask  
  
-   TransferJobsTask  
  
-   TransferObjectsTask  
  
-   TransferDatabaseTask  
  
-   WebServiceTask  
  
-   WmiDataReaderTask  
  
-   WmiEventWatcherTask  
  
-   XMLTask  
  
 如果您倾向于使用更为明确的语法，或您要添加的任务没有 STOCK 名字对象，则您可以使用任务的长名称来向可执行文件添加任务。 此语法还要求您指定任务的版本号。  
  
```csharp  
Executable exec = package.Executables.Add(  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " +  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " +  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91");  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add( _  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " & _  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " & _  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91")  
```  
  
 你可以以编程方式，获取任务的长名称而无需通过使用指定的任务版本中， **AssemblyQualifiedName**类，如下面的示例中所示的属性。 此示例需要引用 Microsoft.SqlServer.SQLTask 程序集。  
  
```csharp  
using Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask;  
...  
      Executable exec = package.Executables.Add(  
        typeof(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName);  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask  
...  
    Dim exec As Executable = package.Executables.Add( _  
      GetType(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName)  
```  
  
 下面的代码示例演示如何创建<xref:Microsoft.SqlServer.Dts.Runtime.Executables>集合从新的包，然后将添加一个文件系统任务和大容量插入任务到该集合，通过使用其**STOCK**名字对象。 此示例需要引用 Microsoft.SqlServer.FileSystemTask 和 Microsoft.SqlServer.BulkInsertTask 程序集。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thBulkInsertTask = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        Console.WriteLine("Type {0}", taskHost.InnerObject.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thBulkInsertTask As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      Console.WriteLine("Type {0}", taskHost.InnerObject.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **示例输出：**  
  
 `Type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
## <a name="taskhost-container"></a>TaskHost 容器  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 类是一个容器，虽然不显示在图形用户界面中，但对于编程非常重要。 此类是所有任务的包装。 使用 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 方法，作为 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 对象添加到包中的任务可转换为 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 对象。 当任务转换为 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 后，您可以对其使用其他属性和方法。 此外，任务本身也可以通过 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 属性访问。 依据您的需求，您可以决定将该任务保留为 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 对象，这样就可以通过 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 集合使用任务的属性。 使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 的优势是可以编写更为通用的代码。 如果您需要特定于任务的代码，则应将任务转换为其适当的对象。  
  
 下面的代码示例演示如何将一个包含 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 的 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> (thBulkInsertTask) 转换为一个 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> 对象。  
  
```csharp  
BulkInsertTask myTask = thBulkInsertTask.InnerObject as BulkInsertTask;  
```  
  
```vb  
Dim myTask As BulkInsertTask = CType(thBulkInsertTask.InnerObject, BulkInsertTask)  
```  
  
 下面的代码示例演示如何将可执行文件转换为 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>，然后使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> 属性确定主机包含的可执行文件的类型。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask1 = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thFileSystemTask2 = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask)  
        {  
          // Do work with FileSystemTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        else if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask)  
        {  
          // Do work with BulkInsertTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        // Add additional statements to check InnerObject, if desired.  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask1 As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thFileSystemTask2 As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      If TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask Then  
        ' Do work with FileSystemTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      ElseIf TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask Then  
        ' Do work with BulkInsertTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      End If  
      ' Add additional statements to check InnerObject, if desired.  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **示例输出：**  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 语句返回一个可执行文件，该文件从新创建的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 对象转换为 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 对象。  
  
 若要对新对象设置属性或调用方法，您有两种选择：  
  
1.  使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 集合。 例如，若要从对象获取一个属性，请使用`th.Properties["propertyname"].GetValue(th))`。 若要设置属性，可使用 `th.Properties["propertyname"].SetValue(th, <value>);`。  
  
2.  将 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 转换为任务类。 例如，若要在将大容量插入任务作为 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> 添加到包中，然后将其转换为 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 之后，再将其转换为 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>，可使用 `BulkInsertTask myTask = th.InnerObject as BulkInsertTask;`。  
  
 在代码中使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 类而不是转换为特定于任务的类具有下列好处：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A>提供程序不需要对在代码中的程序集的引用。  
  
-   您可以编写适用于任何任务的通用例程，因为您无需在编译时知道任务的名称。 这样的通用例程包含的方法中，您向方法传递任务的名称，因此方法代码适用于所有任务。 这是一种编写测试代码的好方法。  
  
 从强制转换<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>到特定于任务的类具有以下优点：  
  
-   Visual Studio 项目提供了你语句结束 (IntelliSense)。  
  
-   代码的运行速度可能会更快。  
  
-   特定于任务的对象允许早期绑定和结果优化。 有关早期绑定和后期绑定的详细信息，请参阅 Visual Basic 语言概念中的主题“早期绑定和后期绑定”。  
  
 下面的代码示例具体阐释了重用任务代码的概念。 该代码示例没有将任务转换为其特定的类等价对象，而是演示了如何将可执行文件转换为 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>，随后使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 编写针对所有任务的通用代码。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package = new Package();  
  
      string[] tasks = { "STOCK:SQLTask", "STOCK:ScriptTask",   
        "STOCK:ExecuteProcessTask", "STOCK:PipelineTask",   
        "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask" };  
  
      foreach (string s in tasks)  
      {  
        TaskHost taskhost = package.Executables.Add(s) as TaskHost;  
        DtsProperties props = taskhost.Properties;  
        Console.WriteLine("Enumerating properties on " + taskhost.Name);  
        Console.WriteLine(" TaskHost.InnerObject is " + taskhost.InnerObject.ToString());  
        Console.WriteLine();  
  
        foreach (DtsProperty prop in props)  
        {  
          Console.WriteLine("Properties for " + prop.Name);  
          Console.WriteLine("Name : " + prop.Name);  
          Console.WriteLine("Type : " + prop.Type.ToString());  
          Console.WriteLine("Readable : " + prop.Get.ToString());  
          Console.WriteLine("Writable : " + prop.Set.ToString());  
          Console.WriteLine();  
        }  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package = New Package()  
  
    Dim tasks() As String = New String() {"STOCK:SQLTask", "STOCK:ScriptTask", _  
              "STOCK:ExecuteProcessTask", "STOCK:PipelineTask", _  
              "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask"}  
  
    For Each s As String In tasks  
  
      Dim taskhost As TaskHost = CType(package.Executables.Add(s), TaskHost)  
      Dim props As DtsProperties = taskhost.Properties  
      Console.WriteLine("Enumerating properties on " & taskhost.Name)  
      Console.WriteLine(" TaskHost.InnerObject is " & taskhost.InnerObject.ToString())  
      Console.WriteLine()  
  
      For Each prop As DtsProperty In props  
        Console.WriteLine("Properties for " + prop.Name)  
        Console.WriteLine(" Name : " + prop.Name)  
        Console.WriteLine(" Type : " + prop.Type.ToString())  
        Console.WriteLine(" Readable : " + prop.Get.ToString())  
        Console.WriteLine(" Writable : " + prop.Set.ToString())  
        Console.WriteLine()  
      Next  
  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>外部资源  
 博客文章[EzAPI – 经过更新以 SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223)，blogs.msdn.com 上的。  

## <a name="see-also"></a>另请参阅  
 [以编程方式连接任务](../../integration-services/building-packages-programmatically/connecting-tasks-programmatically.md)  
  
  

