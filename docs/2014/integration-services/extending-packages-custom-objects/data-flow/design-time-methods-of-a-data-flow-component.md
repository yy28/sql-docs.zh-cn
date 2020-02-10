---
title: 数据流组件的设计时方法 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d7d1a2d3b62578fc2fd627aea32112c218895d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62896257"
---
# <a name="design-time-methods-of-a-data-flow-component"></a>数据流组件的设计时方法
  在执行前，称数据流任务处于设计时状态，因为它将接受增量更改。 这些更改可以包括添加或删除组件、添加或删除连接组件的路径对象以及更改组件的元数据。 出现元数据更改时，组件可监视这些更改并对这些更改作出响应。 例如，组件可以禁止某些更改或为响应某一更改而进行其他更改。 在设计时，设计器通过设计时 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 接口与组件进行交互。  
  
## <a name="design-time-implementation"></a>设计时实现  
 组件的设计时接口通过 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 接口描述。 虽然您不显式实现此接口，但熟悉此接口中定义的方法将有助于您了解 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基类的哪些方法与组件的设计时实例相对应。  
  
 组件加载到 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 后，组件的设计时实例将会被实例化，并会在编辑组件时调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 接口的方法。 基类的实现使您可以只重写您组件需要的方法。 在很多情况下，您可以重写这些方法，以阻止不当的组件编辑。 例如，若要阻止用户向组件中添加输出，可重写 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.InsertOutput%2A> 方法。 否则，当基类调用此方法的实现时，它会向组件中添加一个输出。  
  
 无论组件的用途或功能是什么，您都应重写 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法。 有关 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 的详细信息，请参阅[验证数据流组件](validating-a-data-flow-component.md)。  
  
## <a name="providecomponentproperties-method"></a>ProvideComponentProperties 方法  
 组件的初始化在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法中进行。 此方法在组件添加到数据流任务时由 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器调用，它类似于一个类构造函数。 组件开发人员应该在此方法调用期间创建并初始化该方法的输入、输出和自定义属性。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法不同于构造函数，因为并不是每次实例化组件的设计时实例或运行时实例时都会调用此方法。  
  
 方法的基类实现向组件中添加输入和输出，并向 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 属性分配输入的 ID。 但是，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，未命名基类添加的输入和输出对象。 如果包中的某个组件具有未设置 Name 属性的输入或输出对象，则无法成功加载包。 因此，在使用基实现时，必须对默认输入和输出的 Name 属性显式赋值。  
  
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
>  
  <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> 接口提供对 `Object` 类型的属性值的有限支持。 能够作为自定义属性值存储的唯一对象是简单类型数组，如字符串或整数。  
  
 可指示自定义属性支持属性表达式，方法是从 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.ExpressionType%2A> 枚举将其 `CPET_NOTIFY` 属性的值设置为 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSCustomPropertyExpressionType>，如下列示例中所示。 不必添加用于处理或验证用户输入的属性表达式的任何代码。 可以设置属性的默认值、验证该值并正常读取和使用该值。  
  
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
  
 您可以通过使用<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A>属性来限制用户从枚举中选择自定义属性值，如下面的示例所示，该示例假设您已经定义了一个名为`MyValidValues`的公共枚举。  
  
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
  
 有关详细信息，请参阅 [MSDN 库](https://go.microsoft.com/fwlink/?LinkId=7022)中的“通用类型转换”和“实现类型转换器”。  
  
 可使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 属性指定自定义属性的值的自定义编辑器对话框，如下列示例中所示。 首先，如果无法找到能够满足您需要的现有 UI 类型编辑器，则必须创建从 `System.Drawing.Design.UITypeEditor` 继承的自定义属性编辑器。  
  
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
  
 有关详细信息，请参阅 [MSDN 库](https://go.microsoft.com/fwlink/?LinkId=7022)中的“实现 UI 类型编辑器”。  
  
![Integration Services 图标（小）](../../media/dts-16.gif "集成服务图标（小）")**保持与 Integration Services 最**新  <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [数据流组件的运行时方法](run-time-methods-of-a-data-flow-component.md)  
  
  
