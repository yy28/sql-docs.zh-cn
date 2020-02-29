---
title: 在脚本组件编辑器中配置脚本组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 40f354f190093c0c689e708301bed9fcba8c87c3
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176206"
---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>在脚本组件编辑器中配置脚本组件
  在脚本组件中编写自定义代码之前，必须选择要创建的数据流组件的类型：源、转换或目标，然后在“脚本转换编辑器”中配置组件的元数据和属性  。

## <a name="selecting-the-type-of-component-to-create"></a>选择要创建的组件的类型
 向 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器的“数据流”窗格添加脚本组件时，将显示“选择脚本组件类型”对话框  。 可将组件预配置为源、转换或目标。 进行此初始选择后，可以继续在“脚本转换编辑器”中配置组件  。

 若要设置脚本组件的默认脚本语言，请使用“选项”对话框“常规”页的“脚本语言”选项    。 有关详细信息，请参阅 [General Page](../../general-page-of-integration-services-designers-options.md)。

## <a name="understanding-the-two-design-time-modes"></a>了解两种设计时模式
 在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中，脚本组件具有两种模式：元数据设计模式和代码设计模式。

 打开“脚本转换编辑器”时，组件进入元数据设计模式  。 在此模式下，可以选择输入列，并添加或配置输出和输出列，但不能编写代码。 配置完组件的元数据后，即可切换至代码设计模式编写脚本。

 单击“编辑脚本”切换到代码设计模式时，脚本组件会锁定元数据以防止其他更改，然后根据输入和输出的元数据自动生成基代码  。 完成自动生成代码后，即可输入您的自定义代码。 您的代码使用自动生成的基类来处理输入行、访问缓冲区和缓冲区中的列以及从包中检索连接管理器和变量，所有对象都作为强类型对象处理。

 在代码设计模式下输入完自定义代码后，可以切换回元数据设计模式。 这不会删除您已输入的任何代码；但是，对元数据的后续更改会导致重新生成基类。 然后，您的组件可能无法通过验证，因为自定义代码引用的对象可能已不存在或者已被修改。 在这种情况下，必须手动修复代码，以便能够针对重新生成的基类进行成功编译。

## <a name="configuring-the-component-in-metadata-design-mode"></a>在元数据设计模式下配置组件
 在元数据设计模式下，可以选择输入列，添加和配置输出和输出列，但不能编写代码。 配置完组件的元数据后，即可切换至代码设计模式编写脚本。

 在自定义编辑器中必须要配置的属性取决于脚本组件的用途。 脚本组件可配置为源、转换或目标。 根据其使用方式，该组件可以支持一个输入或多个输出，也可二者都支持。 要编写的自定义代码将处理输入及输出行和列。

### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>脚本转换编辑器的“输入列”页
 对于转换组件和目标组件，将显示“脚本转换编辑器”的“输入列”页；对于源组件则不显示该页   。 在此页中，可以选择希望用于自定义脚本的可用输入列，然后指定可对这些列进行只读还是读/写访问。

 在将要基于此元数据生成的代码项目中，BufferWrapper 项目项包含每个输入的一个类，并且此类包含每个所选输入列的类型化取值函数属性。 `CustomerInput`例如，如果从名为的输入中选择一个整数**CustomerID**列和一个字符串**CustomerName**列，则 BufferWrapper 项目项将包含一个`CustomerInput`派生<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>自的类，并且`CustomerInput`该类将公开一个名为**CustomerID**的整型属性和一个名为**CustomerName**的字符串属性。 使用此约定可编写能够进行类型检查的代码，如下所示：

```vb
Dim currentCustomerID as Integer = CustomerInput.CustomerID
Dim currentCustomerName as String = CustomerInput.CustomerName
```

 有关如何为特定类型的数据流组件配置输入列的详细信息，请参阅[开发特定类型的脚本组件](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)下的相应示例。

### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>脚本转换编辑器的“输入和输出”页
 “脚本转换编辑器”的“输入和输出”页会为源、转换和目标显示   。 在此页中，可以添加、删除和配置要在自定义脚本中使用的输入、输出和输出列，但存在以下限制：

-   用作源时，脚本组件没有输入，支持多个输出。

-   用作转换时，脚本组件支持一个输入和多个输出。

-   用作目标时，脚本组件支持一个输入，没有输出。

 在将要基于此元数据生成的代码项目中，BufferWrapper 项目项包含每个输入和输出的一个类。 例如，如果创建`CustomerOutput`一个名为的输出，BufferWrapper 项目项将包含一个`CustomerOutput`派生自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>的类，并且`CustomerOutput`类将包含所创建的每个输出列的类型化取值函数属性。

 只能在“输入和输出”页中配置输出列  。 可在“输入列”页中选择转换和目标的输入列  。 在 BufferWrapper 项目项中创建的类型化取值函数属性对于输出列来说是只写的。 输入列的取值函数属性将为只读还是读/写取决于在“输入列”页中为每列所选的使用类型  。

 有关如何为特定类型的数据流组件配置输入和输出列的详细信息，请参阅[开发特定类型的脚本组件](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)下的相应示例。

> [!NOTE]
>  虽然您无法在脚本组件中直接将输出配置为错误输出以便自动处理错误行，但必要时可通过创建附加输出并使用脚本将行定向到此输出来再现错误输出的功能。 有关详细信息，请参阅[模拟脚本组件的错误输出](../../data-flow/transformations/script-component.md)。

#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>输出的 ExclusionGroup 和 SynchronousInputID 属性
 
  `ExclusionGroup` 属性仅在具有同步输出的转换中具有非零值，其中您的代码要执行筛选或分支跳转，并将每一行定向到共享同一非零 `ExclusionGroup` 值的输出之一。 例如，转换可将行定向到默认输出或错误输出。 在此方案中，如果您创建附加输出，请确保将 `SynchronousInputID` 属性的值设置为与组件的输入 `ID` 相匹配的整数。

 
  `SynchronousInputID` 属性仅在具有同步输出的转换中具有非零值。 如果此属性的值为零，则意味着输出是异步的。 对于同步输出，行将传递给所选一个或多个输出而不添加任何新行，此属性应包含组件的输入 `ID`。

> [!NOTE]
>  当 "**脚本转换编辑器**" 创建第一个输出时，该编辑器`SynchronousInputID`会将输出的属性设置`ID`为组件的输入的。 但是，当编辑器创建后续输出时，它会将那些输出的 `SynchronousInputID` 属性设置为零。
> 
>  如果要创建具有同步输出的组件，则每个输出的`SynchronousInputID`属性必须设置为`ID`组件的输入的。 因此，编辑器在第一个输出之后创建的每个输出的 `SynchronousInputID` 值必须从零更改为组件的输入 `ID`。
> 
>  如果您创建的是具有异步输出的组件，则每个输出的 `SynchronousInputID` 属性必须设置为零。 因此，第一个输出必须将其`SynchronousInputID`值从`ID`组件输入的更改为零。

 有关将行定向到脚本组件中两个同步输出之一的示例，请参阅[使用脚本组件创建同步转换](../../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)。

### <a name="object-names-in-generated-script"></a>生成的脚本中的对象名称
 脚本组件会分析输入和输出的名称，还会分析输入和输出中的列的名称，并基于这些名称在 BufferWrapper 项目项中生成类和属性。 如果找到的名称包含不属于 Unicode 类别 `UppercaseLetter`、`LowercaseLetter`、`TitlecaseLetter`、`ModifierLetter`、`OtherLetter` 或 `DecimalDigitLetter` 的字符，则生成的名称中的无效字符将被删除。 例如，空格将被删除，因此名称为 FirstName 和 [First Name] 的两个输入列都会解释为具有列名 FirstName，从而产生不可预测的结果    。 为了避免发生这种情况，脚本组件所使用的输入和输出的名称以及输入列和输出列的名称应仅包含本部分列出的 Unicode 类别中的字符。

### <a name="script-page-of-the-script-transformation-editor"></a>脚本转换编辑器的“脚本”页
 在“脚本任务编辑器”的“脚本”页中，可以为脚本任务指定唯一的名称和说明   。 还可以为以下属性赋值。

> [!NOTE]
>  在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 和更高版本中，所有脚本都将预编译。 在早期版本中，通过设置任务的 `Precompile` 属性来指定是否对脚本进行预编译。

#### <a name="validateexternalmetadata-property"></a>ValidateExternalMetadata 属性
 
  `ValidateExternalMetadata` 属性的布尔值指定组件是应在设计时针对外部数据源执行验证，还是应推迟到运行时才验证。 默认情况下，此属性的值为 `True`；也就是说，在设计时和运行时都对外部元数据进行验证。 如果外部数据源在设计时不可用，可以将此属性的值设置为 `False`；例如，当包仅在运行时下载源或创建目标时。

#### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 和 ReadWriteVariables 属性
 可以输入以逗号分隔的现有变量列表作为这些属性的值，使这些变量在脚本组件代码中可用于只读或读/写访问。 这些变量可在代码中通过自动生成的基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> 属性来访问。 有关详细信息，请参阅[在脚本组件中使用变量](using-variables-in-the-script-component.md)。

> [!NOTE]
>  变量名称区分大小写。

#### <a name="scriptlanguage"></a>ScriptLanguage
 您可以选择 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 作为脚本组件的编程语言。

#### <a name="edit-script-button"></a>“编辑脚本”按钮
 使用“编辑脚本”按钮可打开 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE，你可以在其中编写自定义脚本  。 有关详细信息，请参阅[脚本组件的编码和调试](coding-and-debugging-the-script-component.md)。

### <a name="connection-managers-page-of-the-script-transformation-editor"></a>脚本转换编辑器的“连接管理器”页
 在“脚本转换编辑器”的“连接管理器”页中，可以添加和删除要在自定义脚本中使用的连接管理器   。 通常，创建源或目标组件时需要引用连接管理器。

 在将要基于此元数据生成的代码项目中，`ComponentWrapper` 项目项包含一个 `Connections` 集合类，该类为每个所选连接管理器包含一个类型化取值函数属性。 每个类型化取值函数属性的名称都与连接管理器本身的名称相同，该属性将返回对作为 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> 实例的连接管理器的引用。 例如，如果已在编辑器的“连接管理器”页中添加名为 `MyADONETConnection` 的连接管理器，则可在脚本中使用以下代码获取对该连接管理器的引用  ：

```vb
Dim myADONETConnectionManager As IDTSConnectionManager100 = _
    Me.Connections.MyADONETConnection
```

 有关详细信息，请参阅[在脚本组件中连接数据源](connecting-to-data-sources-in-the-script-component.md)。

![Integration Services 图标（小）](../../media/dts-16.gif "集成服务图标（小）")**保持与 Integration Services 最**新  <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。

## <a name="see-also"></a>另请参阅
 [脚本组件的编码和调试](coding-and-debugging-the-script-component.md)


