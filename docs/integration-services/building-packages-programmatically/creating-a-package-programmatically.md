---
title: "以编程方式创建包 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
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
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: e44bcc70-32d3-43e8-a84b-29aef819d5d3
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 58a8201d68cb6d942bd98ca3c53b6cf98336284e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-package-programmatically"></a>以编程方式创建包
  <xref:Microsoft.SqlServer.Dts.Runtime.Package> 对象是 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 项目解决方案中的所有其他对象的顶级容器。 作为顶级容器，包是第一个创建的对象，并将后续对象添加到该包，然后在包的上下文中执行这些对象。 包本身并不移动或转换数据。 包依靠自己包含的任务执行工作。 任务执行大多数由包执行的工作，并定义包的功能。 只需三行代码即可完成包的创建和执行，但需要向包中添加各种任务和 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 对象以增加其功能。 本节讨论如何以编程方式创建包。 不提供有关如何创建任务或 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 的信息。 有关信息，请参阅后续相关章节。  
  
## <a name="example"></a>示例  
 若要使用 Visual Studio IDE 编写代码，需要对 Microsoft.SqlServer.ManagedDTS.DLL 的引用，以便创建针对 Microsoft.SqlServer.Dts.Runtime 的 `using` 语句（在 Visual Basic .NET 中为 `Imports`）。 下面的代码示例演示如何创建一个空包。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package;  
      package = new Package();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package  
    package = New Package  
  
  End Sub  
  
End Module  
```  
  
 若要编译并运行该示例，请在 Visual Studio 中按 F5。 若要生成使用 C# 编译器，代码**csc.exe**、 在命令提示符下进行编译，使用以下命令和文件引用，替换 *\<filename >* .cs 或.vb 文件中，并为其提供的名称与 *\<outputfilename >*所选。  
  
 **csc /target: library /out: \<outputfilename >.dll\<文件名 >.cs /r:Microsoft.SqlServer.Managed DTS.dll"/r:System.dll**  
  
 若要生成使用 Visual Basic.NET 编译器中，代码**vbc.exe**、 在命令提示符下进行编译，使用以下命令和文件引用。  
  
 **vbc /target: library /out: \<outputfilename >.dll\<文件名 >.vb /r:Microsoft.SqlServer.Managed DTS.dll"/r:System.dll**  
  
 还可以通过将存储在磁盘中的现有包加载到文件系统或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中来创建包。 差异在于<xref:Microsoft.SqlServer.Dts.Runtime.Application>首次创建对象，和包对象内容由应用程序的重载方法之一： **LoadPackage**平面文件的**LoadFromSQLServer**包保存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>包保存到文件系统。 下面的示例从磁盘加载一个现有包，然后查看该包的多个属性。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class ApplicationTests  
  {  
    static void Main(string[] args)  
    {  
      // The variable pkg points to the location of the  
      // ExecuteProcess package sample that was installed with  
      // the SSIS samples.  
      string pkg = @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx";  
  
      Application app = new Application();  
      Package p = app.LoadPackage(pkg, null);  
  
      // Now that the package is loaded, we can query on  
      // its properties.  
      int n = p.Configurations.Count;  
      DtsProperty p2 = p.Properties["VersionGUID"];  
      DTSProtectionLevel pl = p.ProtectionLevel;  
  
      Console.WriteLine("Number of configurations = " + n.ToString());  
      Console.WriteLine("VersionGUID = " + (string)p2.GetValue(p));  
      Console.WriteLine("ProtectionLevel = " + pl.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module ApplicationTests  
  
  Sub Main()  
  
    ' The variable pkg points to the location of the  
    ' ExecuteProcess package sample that was installed with  
    ' the SSIS samples.  
    Dim pkg As String = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx"  
  
    Dim app As Application = New Application()  
    Dim p As Package = app.LoadPackage(pkg, Nothing)  
  
    ' Now that the package is loaded, we can query on  
    ' its properties.  
    Dim n As Integer = p.Configurations.Count  
    Dim p2 As DtsProperty = p.Properties("VersionGUID")  
    Dim pl As DTSProtectionLevel = p.ProtectionLevel  
  
    Console.WriteLine("Number of configurations = " & n.ToString())  
    Console.WriteLine("VersionGUID = " & CType(p2.GetValue(p), String))  
    Console.WriteLine("ProtectionLevel = " & pl.ToString())  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **示例输出：**  
  
 `Number of configurations = 2`  
  
 `VersionGUID = {09016682-89B8-4406-AAC9-AF1E527FF50F}`  
  
 `ProtectionLevel = DontSaveSensitive`  
  
## <a name="external-resources"></a>外部资源  
  
-   博客文章[API 示例-OleDB 源和 OleDB 目标](http://go.microsoft.com/fwlink/?LinkId=220824)，blogs.msdn.com 上的。  
  
-   博客文章[EzAPI – 经过更新以 SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223)，blogs.msdn.com 上的。  
  
## <a name="see-also"></a>另請參閱  
 [以编程方式添加任务](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)  
  
  

