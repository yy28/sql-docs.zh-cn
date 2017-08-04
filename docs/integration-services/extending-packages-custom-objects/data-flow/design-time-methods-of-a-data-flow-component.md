---
title: "设计时方法的数据进行流处理组件 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- custom data flow components [Integration Services], method execution sequence
- ProcessInput method
- method execution sequence [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], method execution sequence
ms.assetid: b5a121a1-b87c-441b-a42c-2cec628dc81c
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf248d93b1b1e581c3315cde9b1f96edc58bcfde
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="design-time-methods-of-a-data-flow-component"></a>数据流组件的设计时方法
  在执行前，称数据流任务处于设计时状态，因为它将接受增量更改。 这些更改可以包括添加或删除组件、添加或删除连接组件的路径对象以及更改组件的元数据。 出现元数据更改时，组件可监视这些更改并对这些更改作出响应。 例如，一个组件可以禁止进行某些更改或进行更改，以响应更改。 在设计时，设计器通过设计时 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 接口与组件进行交互。  
  
## <a name="design-time-implementation"></a>设计时实现  
 组件的设计时接口通过 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 接口描述。 虽然您不显式实现此接口，但熟悉此接口中定义的方法将有助于您了解 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基类的哪些方法与组件的设计时实例相对应。  
  
 组件加载到 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 后，组件的设计时实例将会被实例化，并会在编辑组件时调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 接口的方法。 基类的实现使您可以只重写您组件需要的方法。 在很多情况下，您可以重写这些方法，以阻止不当的组件编辑。 例如，若要阻止用户向组件中添加输出，可重写 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.InsertOutput%2A> 方法。 否则，当基类调用此方法的实现时，它会向组件中添加一个输出。  
  
 无论组件的用途或功能是什么，您都应重写 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法。 有关详细信息<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>和<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>，请参阅[验证数据流组件](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)。  
  
## <a name="providecomponentproperties-method"></a>ProvideComponentProperties 方法  
 组件的初始化在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法中进行。 此方法在组件添加到数据流任务时由 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器调用，它类似于一个类构造函数。 组件开发人员应该在此方法调用期间创建并初始化该方法的输入、输出和自定义属性。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法不同于构造函数，因为并不是每次实例化组件的设计时实例或运行时实例时都会调用此方法。  
  
 方法的基类实现向组件中添加输入和输出，并向 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 属性分配输入的 ID。 但是，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，未命名基类添加的输入和输出对象。 包含输入组件的包或多个输出对象未设置其 Name 属性不会成功加载。 因此，当你使用的基实现，你必须显式分配值为 Name 属性的默认输入和输出。  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    /// TODO: Reset the component.  
    /// TODO: Add custom properties.  
    /// TODO: Add input objects.  
    /// TODO: Add output objects.  
}  
```  
  
```vb  
Public Overrides Sub ProvideComponentProperties()  
    ' TODO: Reset the component.  
    ' TODO: Add custom properties.  
    ' TODO: Add input objects.  
    ' TODO: Add output objects.  
End Sub  
```  
  
### <a name="creating-custom-properties"></a>创建自定义属性  
 在对 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法的调用中，组件开发人员应该向组件添加自定义属性 (<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100>)。 自定义属性没有数据类型属性。 自定义属性的数据类型由值的数据类型设置，您已将该数据类型分配给其 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.Value%2A> 属性。 但是，在向自定义属性分配初始值后，不能分配具有其他数据类型的值。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100>接口具有对有限的支持类型的属性值**对象**。 能够作为自定义属性值存储的唯一对象是简单类型数组，如字符串或整数。  
  
 可以自定义属性的值设置支持属性表达式来指示其<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.ExpressionType%2A>属性**CPET_NOTIFY**从<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSCustomPropertyExpressionType>枚举，如下面的示例中所示。 不必添加用于处理或验证用户输入的属性表达式的任何代码。 可以设置属性的默认值、验证该值并正常读取和使用该值。  
  
```csharp  
IDTSCustomProperty100 myCustomProperty;  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY;  
```  
  
```vb  
Dim myCustomProperty As IDTSCustomProperty100  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY  
```  
  
 您可以将用户限制到通过使用枚举中定义自定义属性值<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A>属性，如下面的示例，假设你已经定义了名为公共枚举中所示**MyValidValues**。  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the type with the custom property.  
customProperty.TypeConverter = typeof(MyValidValues).AssemblyQualifiedName;  
// Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne;    
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the type with the custom property.  
customProperty.TypeConverter = GetType(MyValidValues).AssemblyQualifiedName   
' Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne  
```  
  
 有关详细信息，请参阅"通用类型转换"和"实现类型转换器"中[MSDN 库](http://go.microsoft.com/fwlink/?LinkId=7022)。  
  
 可使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 属性指定自定义属性的值的自定义编辑器对话框，如下列示例中所示。 首先，你必须创建自定义类型继承自的编辑器**System.Drawing.Design.UITypeEditor**，如果找不到适合你需要的现有 UI 类型编辑器类。  
  
```csharp  
public class MyCustomTypeEditor : UITypeEditor  
{  
...  
}  
```  
  
```vb  
Public Class MyCustomTypeEditor  
  Inherits UITypeEditor   
  ...  
End Class  
```  
  
 然后，指定此类作为自定义属性的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 属性的值。  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the editor with the custom property.  
customProperty.UITypeEditor = typeof(MyCustomTypeEditor).AssemblyQualifiedName;  
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the editor with the custom property.  
customProperty.UITypeEditor = GetType(MyCustomTypeEditor).AssemblyQualifiedName  
```  
  
 详细信息，请参阅"实现 UI 类型编辑器"中[MSDN 库](http://go.microsoft.com/fwlink/?LinkId=7022)。  
  
## <a name="see-also"></a>另請參閱  
 [数据流组件的运行时方法](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
  
  
