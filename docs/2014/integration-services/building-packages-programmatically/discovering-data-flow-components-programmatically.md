---
title: 以编程方式发现数据流组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- PipelineComponentInfos collection
- data flow task [Integration Services], components
- discovering data flow components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: ff92a96a-8af6-4532-82cc-c0bbff92401b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e2de2129e268cf749f14bf6c8167de9ef66d516e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055758"
---
# <a name="discovering-data-flow-components-programmatically"></a>以编程方式查找数据流组件
  向包中添加数据流任务后，下一步是确定可用的数据流组件。 可以用编程方式查找本地计算机上安装并且可用的数据流源、转换和目标。 有关向包添加数据流任务的信息，请参阅[以编程方式添加数据流任务](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)。  
  
## <a name="discovering-components"></a>查找组件  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 类提供 <xref:Microsoft.SqlServer.Dts.Runtime.Application.PipelineComponentInfos%2A> 集合，该集合包含在本地计算机上正确安装的每个组件的 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 对象。 每个 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 都包含有关组件的信息，如组件的名称、说明和创建名称。 可在向包中添加组件时使用 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> 属性中返回的值来设置 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 属性。  
  
## <a name="next-step"></a>下一步  
 发现可用组件后，下一步是添加和配置这些组件，这将在下一主题[以编程方式添加数据流任务](../building-packages-programmatically/adding-data-flow-components-programmatically.md)中讨论。  
  
## <a name="sample"></a>示例  
 下面的代码示例演示如何枚举 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfos> 对象的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 集合，从而以编程方式查找本地计算机上的可用数据流组件。 此示例需要引用 Microsoft.SqlServer.ManagedDTS 程序集。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application application = new Application();  
      PipelineComponentInfos componentInfos = application.PipelineComponentInfos;  
  
      foreach (PipelineComponentInfo componentInfo in componentInfos)  
      {  
        Console.WriteLine("Name: " + componentInfo.Name + "\n" +  
          " CreationName: " + componentInfo.CreationName + "\n");  
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
  
    Dim application As Application = New Application()  
  
    Dim componentInfos As PipelineComponentInfos = application.PipelineComponentInfos  
  
    For Each componentInfo As PipelineComponentInfo In componentInfos  
      Console.WriteLine("Name: " & componentInfo.Name & vbCrLf & _  
        " CreationName: " & componentInfo.CreationName & vbCrLf)  
    Next  
  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [以编程方式添加数据流组件](../building-packages-programmatically/adding-data-flow-components-programmatically.md)  
  
  
