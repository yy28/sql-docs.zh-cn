---
title: 创建自定义数据流组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- design-time component interface [Integration Services]
- custom data flow components [Integration Services], about data flow components
- custom data flow components [Integration Services]
- data flow components [Integration Services]
- data flow components [Integration Services], developing
ms.assetid: 9d96bcf5-eba8-44bd-b113-ed51ad0d0521
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 93a2d0db91c8e22146ed3d83bf30d72d9cc3a00e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297289"
---
# <a name="creating-a-custom-data-flow-component"></a>创建自定义数据流组件

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中，数据流任务公开一个对象模型，该对象模型允许开发人员使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 和托管代码创建自定义数据流组件：源、转换和目标。  
  
 数据流任务由包含 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 接口和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 对象集合的组件组成，这些对象定义组件之间的数据移动。  
  
> [!NOTE]  
>  在您创建自定义提供程序时，需要使用元数据列值更新 ProviderDescriptors.xml 文件。  
  
## <a name="design-time-and-run-time"></a>设计时和运行时  
 在执行前，称数据流任务处于设计时状态，因为它将接受增量更改。 这些更改可以包括添加或删除组件、添加或删除连接组件的路径对象以及更改组件的元数据。 出现元数据更改时，组件可监视这些更改并对这些更改作出响应。 例如，组件可以禁止某些更改或为响应某一更改而进行其他更改。 在设计时，设计器通过设计时 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 接口与组件进行交互。  
  
 在执行时，数据流任务将检查一系列组件、准备执行计划以及管理执行工作计划的工作线程池。 虽然每个工作线程都执行数据流任务的一些内部工作，但工作线程的主要任务是通过运行时 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> 接口调用组件的方法。  
  
## <a name="creating-a-component"></a>创建组件  
 若要创建数据流组件，可从 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基类派生类，再应用 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 类，然后重写适当的基类方法。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 实现 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> 接口，并公开这些接口的方法，供您在组件中重写。  
  
 根据您的组件所使用的对象，您的项目将需要引用以下部分或全部程序集：  
  
|功能|要引用的程序集|要导入的命名空间|  
|-------------|---------------------------|-------------------------|  
|设计器中|Microsoft.SqlServer.PipelineHost|<xref:Microsoft.SqlServer.Dts.Pipeline>|  
|数据流包装|Microsoft.SqlServer.DTSPipelineWrap|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>|  
|运行时|Microsoft.SQLServer.ManagedDTS|<xref:Microsoft.SqlServer.Dts.Runtime>|  
|运行时包装|Microsoft.SqlServer.DTSRuntimeWrap|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper>|  
  
 下面的代码示例演示了一个简单的组件，该组件从基类派生，并应用 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>。 需要添加对 Microsoft.SqlServer.DTSPipelineWrap 程序集的引用。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SampleComponent", ComponentType = ComponentType.Transform )]  
    public class BasicComponent: PipelineComponent  
    {  
        // TODO: Override the base class methods.  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="SampleComponent", ComponentType:=ComponentType.Transform)> _  
Public Class BasicComponent  
  
    Inherits PipelineComponent  
  
    ' TODO: Override the base class methods.  
  
End Class  
```  
  
## <a name="see-also"></a>另请参阅  
 [为数据流组件开发用户界面](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
  
  
