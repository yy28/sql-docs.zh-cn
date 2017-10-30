---
title: "开发使用多个输入数据流组件 |Microsoft 文档"
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
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2cafe3a18fbe930088347304ed758afe505771d6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>开发具有多个输入的数据流组件
  如果其多个输入以不相等速率生成数据，则具有多个输入的数据流组件可能会占用过多的内存。 当你开发自定义数据流组件支持两个或多个输入时，你可以管理此内存压力 Microsoft.SqlServer.Dts.Pipeline 命名空间中使用以下成员：  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 属性。 设置此属性的值**true**如果你想要实现的代码所需的你自定义数据流组件来管理数据以不相等速率流动。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。 你必须提供此方法的实现，如果你设置<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>属性**true**。 如果未提供某一实现方式，则数据流引擎将在运行时引发异常。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。 你还必须提供此方法的实现，如果你设置<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>属性**true**和自定义组件支持两个以上的输入。 如果未提供某一实现方式，且用户附加多个输入，则数据流引擎将在运行时将引发异常。  
  
 这些成员一起使您能够开发一个解决方案来解决内存压力，该解决方案类似于 Microsoft 为合并转换和合并联接转换开发的解决方案。  
  
## <a name="setting-the-supportsbackpressure-property"></a>设置 SupportsBackPressure 属性  
 若要设置的值的自定义数据流组件支持多个输入为实现更好的内存管理的第一步<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>属性**true**中<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>。 时的值<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>是**true**，数据流引擎调用<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>方法，当存在两个以上的输入时，还会调用<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>方法在运行时。  
  
### <a name="example"></a>示例  
 在下面的示例中，实现<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>设置的值<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>到**true**。  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>实现 IsInputReady 方法  
 当你设置的值<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>属性**true**中<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>对象，你还必须提供的实现<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>类。  
  
> [!NOTE]  
>  您的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法的实现方式不应在基类中调用这些实现方式。 此方法的基中的默认实现类所只需引发**NotImplementedException**。  
  
 当实现此方法时，将元素的状态设置中的布尔值*canProcess*数组的每个组件的输入。 (输入由其 ID 值*inputIDs*数组。)当你设置的值中的某个元素*canProcess*数组到**true**输入，数据流引擎调用该组件的<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>方法，并为指定的输入提供更多的数据。  
  
 可用，更多的上游数据时的值*canProcess*至少一个输入的数组元素必须始终为**true**，或处理停止。  
  
 数据流引擎将在发送每个数据缓冲区前调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法，以便确定哪些输入正在等待接收更多数据。 在返回值指示某个输入被阻塞时，数据流引擎暂时为该输入缓存附加的数据缓冲区，而不是将它们发送到该组件。  
  
> [!NOTE]  
>  您不必在自己的代码中调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 数据流引擎调用这些方法和其他方法的**PipelineComponent**时您重写，数据流引擎运行你的组件的类。  
  
### <a name="example"></a>示例  
 在下面的示例中，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法的实现方式指示在以下条件成立时某个输入正在等待接收更多数据：  
  
-   更多的上游数据可用于该输入 (`!inputEOR`)。  
  
-   在已接收该组件的缓冲区中，对于该输入该组件当前不具有可供处理的数据 (`inputBuffers[inputIndex].CurrentRow() == null`)。  
  
 如果输入正在等待接收更多的数据，数据流组件指示这通过将设置为**true**中的元素的值*canProcess*对应于该输入的数组。  
  
 相反，在该组件对于该输入仍具有可供处理的数据时，该示例将挂起对该输入的处理。 该示例执行这通过将设置为**false**中的元素的值*canProcess*对应于该输入的数组。  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 前面的示例使用布尔型 `inputEOR` 数组指示是否有更多的上游数据可用于每个输入。 该数组名称中的 `EOR` 表示“行集结束”，并且引用数据流缓冲区的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 属性。 在此处未包括的示例部分中，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法为它接收的每个数据缓冲区检查 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 属性的值。 值时**true**指示没有可用于输入的没有更多的上游数据，该示例设置的值`inputEOR`到该输入的数组元素**true**。 此示例的<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>方法设置中的相应元素的值*canProcess*数组到**false**输入时的值`inputEOR`数组元素表示没有可用于输入的没有更多的上游数据。  
  
## <a name="implementing-the-getdependentinputs-method"></a>实现 GetDependentInputs 方法  
 在您的自定义数据流组件支持多个输入时，您还必须为 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法提供实现方式。  
  
> [!NOTE]  
>  您的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法的实现方式不应在基类中调用这些实现方式。 此方法的基中的默认实现类所只需引发**NotImplementedException**。  
  
 在用户将多个输入附加到组件时，数据流引擎仅调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 如果组件具有只有两个输入和<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>方法指示一个输入被阻止 (*canProcess* = **false**)，数据流引擎知道另一个输入是等待接收更多的数据。 但是，在存在多个输入，并且 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法指示一个输入被阻塞时，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 中的附加代码标识哪些输入正在等待接收更多数据。  
  
> [!NOTE]  
>  您不必在自己的代码中调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 数据流引擎调用这些方法和其他方法的**PipelineComponent**时您重写，数据流引擎运行你的组件的类。  
  
### <a name="example"></a>示例  
 对于被阻塞的特定输入，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法的以下实现方式返回正在等待接收更多数据、并因此阻塞指定输入的输入集合。 该组件通过检查在已接收组件的缓冲区中是否存在当前没有可供处理的数据的输入（但并非已阻塞的输入）(`inputBuffers[i].CurrentRow() == null`)，标识正在阻塞的输入 。 然后，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法将正在阻塞的输入的集合以输入 ID 的集合的形式返回。  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  

