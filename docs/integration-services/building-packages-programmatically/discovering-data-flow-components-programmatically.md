---
title: "以编程方式发现数据流组件 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
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
- PipelineComponentInfos collection
- data flow task [Integration Services], components
- discovering data flow components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: ff92a96a-8af6-4532-82cc-c0bbff92401b
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 78090618d5025a6ab29c888d09db44ddfff278fa
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="discovering-data-flow-components-programmatically"></a>以编程方式查找数据流组件
  向包中添加数据流任务后，下一步是确定可用的数据流组件。 可以用编程方式查找本地计算机上安装并且可用的数据流源、转换和目标。 有关向包添加数据流任务的信息，请参阅[数据数据流任务以编程方式添加](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)。  
  
## <a name="discovering-components"></a>查找组件  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 类提供 <xref:Microsoft.SqlServer.Dts.Runtime.Application.PipelineComponentInfos%2A> 集合，该集合包含在本地计算机上正确安装的每个组件的 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 对象。 每个 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 都包含有关组件的信息，如组件的名称、说明和创建名称。 可在向包中添加组件时使用 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> 属性中返回的值来设置 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 属性。  
  
## <a name="next-step"></a>下一步  
 在发现可用的组件之后, 的下一步是添加和配置组件，在下一步的主题中，对其进行讨论[添加数据数据流组件以编程方式](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)。  
  
## <a name="sample"></a>示例  
 下面的代码示例演示如何枚举 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfos> 对象的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 集合，从而以编程方式查找本地计算机上的可用数据流组件。 此示例要求 Microsoft.SqlServer.ManagedDTS 程序集的引用。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [以编程方式添加数据流组件](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)  
  
  

