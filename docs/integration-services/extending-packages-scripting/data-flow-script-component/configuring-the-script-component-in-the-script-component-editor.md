---
title: "配置脚本组件编辑器中的脚本组件 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
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
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8488fcc7d402430f66b9b9018b31956a5a1d8383
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>在脚本组件编辑器中配置脚本组件
  脚本组件中编写自定义代码之前，您必须选择你想要创建的数据流组件的类型-源、 转换或目标，然后配置该组件的元数据和中的属性**脚本转换编辑器**。  
  
## <a name="selecting-the-type-of-component-to-create"></a>选择要创建的组件的类型  
 当将脚本组件添加到的数据流窗格[!INCLUDE[ssIS](../../../includes/ssis-md.md)]设计器中，**选择脚本组件类型**对话框随即出现。 可将组件预配置为源、转换或目标。 进行此初始选择后，你可以继续配置中的组件**脚本转换编辑器**。  
  
 若要设置脚本组件的默认脚本语言，使用**脚本语言**选项**常规**页**选项**对话框。 有关详细信息，请参阅 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
## <a name="understanding-the-two-design-time-modes"></a>了解两种设计时模式  
 在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中，脚本组件具有两种模式：元数据设计模式和代码设计模式。  
  
 当你打开**脚本转换编辑器**，组件会输入元数据设计模式。 在此模式下，可以选择输入列，并添加或配置输出和输出列，但不能编写代码。 配置组件的元数据后，你可以切换到代码设计模式以编写脚本。  
  
 当你切换到代码设计模式通过单击**编辑脚本**，脚本组件锁定元数据以防止其他更改，然后从输入和输出的元数据自动生成基代码。 完成自动生成代码后，即可输入您的自定义代码。 您的代码使用自动生成的基类来处理输入行、访问缓冲区和缓冲区中的列以及从包中检索连接管理器和变量，所有对象都作为强类型对象处理。  
  
 在代码设计模式下输入完自定义代码后，可以切换回元数据设计模式。 这不会删除您已输入的任何代码；但是，对元数据的后续更改会导致重新生成基类。 然后，您的组件可能无法通过验证，因为自定义代码引用的对象可能已不存在或者已被修改。 在这种情况下，必须手动修复代码，以便能够针对重新生成的基类进行成功编译。  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>在元数据设计模式下配置组件  
 在元数据设计模式下，可以选择输入列，添加和配置输出和输出列，但不能编写代码。 配置完组件的元数据后，即可切换至代码设计模式编写脚本。  
  
 在自定义编辑器中必须要配置的属性取决于脚本组件的用途。 脚本组件可配置为源、转换或目标。 根据其使用方式，该组件可以支持一个输入或多个输出，也可二者都支持。 要编写的自定义代码将处理输入及输出行和列。  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>脚本转换编辑器的“输入列”页  
 **输入列**页**脚本转换编辑器**有关转换和目标，而不是源显示。 在此页中，可以选择希望用于自定义脚本的可用输入列，然后指定可对这些列进行只读还是读/写访问。  
  
 在将要基于此元数据生成的代码项目中，BufferWrapper 项目项包含每个输入的一个类，并且此类包含每个所选输入列的类型化取值函数属性。 例如，如果你选择一个整数**CustomerID**列和字符串**CustomerName**从名为的输入列**CustomerInput**，BufferWrapper 项目项将包含**CustomerInput**派生自的类<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>，和**CustomerInput**类将公开名为是整数属性**CustomerID**和名为的字符串属性**CustomerName**。 使用此约定可编写能够进行类型检查的代码，如下所示：  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 有关如何配置为特定类型的数据流组件的输入的列的详细信息，请参阅下的相应实例[开发特定 Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>脚本转换编辑器的“输入和输出”页  
 **输入和输出**页**脚本转换编辑器**显示有关源、 转换和目标。 在此页中，可以添加、删除和配置要在自定义脚本中使用的输入、输出和输出列，但存在以下限制：  
  
-   用作源时，脚本组件没有输入，支持多个输出。  
  
-   用作转换时，脚本组件支持一个输入和多个输出。  
  
-   用作目标时，脚本组件支持一个输入，没有输出。  
  
 在将要基于此元数据生成的代码项目中，BufferWrapper 项目项包含每个输入和输出的一个类。 例如，如果创建名为输出**CustomerOutput**，BufferWrapper 项目项将包含**CustomerOutput**派生自的类<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>，和**CustomerOutput**类将包含创建每个输出列的类型化访问器属性。  
  
 你可以输出列仅在配置**输入和输出**页。 你可以选择输入的列转换和目标上**输入列**页。 在 BufferWrapper 项目项中创建的类型化取值函数属性对于输出列来说是只写的。 输入列的访问器属性将为只读或读/写，具体取决于您选择为每个列的使用类型**输入列**页。  
  
 有关配置的特定类型的数据输入和输出数据流组件，请参阅下的相应实例[开发特定 Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。  
  
> [!NOTE]  
>  虽然您无法在脚本组件中直接将输出配置为错误输出以便自动处理错误行，但必要时可通过创建附加输出并使用脚本将行定向到此输出来再现错误输出的功能。 有关详细信息，请参阅[脚本组件为模拟错误输出](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>输出的 ExclusionGroup 和 SynchronousInputID 属性  
 **ExclusionGroup**属性仅在与同步输出，其中你的代码将执行筛选或分支和每个将行定向到一个共用同一个非零输出的转换中具有非零值**ExclusionGroup**值。 例如，转换可将行定向到默认输出或错误输出。 当你创建此方案的其他输出时，请确保设置的值**SynchronousInputID**属性匹配的整数**ID**的组件的输入。  
  
 **SynchronousInputID**属性仅在与同步输出的转换中具有非零值。 如果此属性的值为零，则意味着输出是异步的。 为同步输出，其中行都被传递到所选的输出或输出而无需添加任何新行，此属性应包含**ID**的组件的输入。  
  
> [!NOTE]  
>  当**脚本转换编辑器**创建第一个输出，编辑器集**SynchronousInputID**属性将输出发送到**ID**的组件的输入。 但是，当编辑器创建后续输出时，编辑器将设置**SynchronousInputID**为零这些输出属性。  
>   
>  如果你创建的组件与同步输出，每个输出必须具有其**SynchronousInputID**属性设置为**ID**的组件的输入。 因此，每个输出编辑器创建后的第一个输出中必须有其**SynchronousInputID**值从 0 更改为**ID**的组件的输入。  
>   
>  如果创建的具有异步输出的组件，必须具有每个输出其**SynchronousInputID**属性设置为零。 因此，第一个输出必须具有其**SynchronousInputID**值更改，不再**ID**的组件的输入为零。  
  
 将两个同步输出之一的行定向脚本组件中的示例，请参阅[使用脚本组件创建同步转换](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)。  
  
### <a name="object-names-in-generated-script"></a>生成的脚本中的对象名称  
 脚本组件会分析输入和输出的名称，还会分析输入和输出中的列的名称，并基于这些名称在 BufferWrapper 项目项中生成类和属性。 如果找到的名称包含不属于 Unicode 类别的字符**UppercaseLetter**， **LowercaseLetter**， **TitlecaseLetter**， **ModifierLetter**， **OtherLetter**，或**DecimalDigitLetter**，无效的字符被放置在生成的名称。 例如，空格被删除，因此两个输入列具有名称**FirstName**和 [**名字**] 被解释为具有列名称**FirstName**，结果不可预知。 为了避免发生这种情况，脚本组件所使用的输入和输出的名称以及输入列和输出列的名称应仅包含本部分列出的 Unicode 类别中的字符。  
  
### <a name="script-page-of-the-script-transformation-editor"></a>脚本转换编辑器的“脚本”页  
 上**脚本**页**脚本任务编辑器**，分配一个唯一的名称和描述脚本任务。 还可以为以下属性赋值。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 和更高版本中，所有脚本都将预编译。 在以前版本中，指定脚本是否已通过设置预编译**Precompile**任务的属性。  
  
#### <a name="validateexternalmetadata-property"></a>ValidateExternalMetadata 属性  
 布尔值**ValidateExternalMetadata**属性指定是否组件应执行验证对外部数据源在设计时，或是否它应将推迟到运行时验证。 默认情况下，此属性的值是**True**; 即，在设计时和运行时验证外部元数据。 你可能想要设置到此属性的值**False**当外部数据源不可用在设计时： 例如，当包下载源或创建仅在运行时的目标。  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 和 ReadWriteVariables 属性  
 可以输入以逗号分隔的现有变量列表作为这些属性的值，使这些变量在脚本组件代码中可用于只读或读/写访问。 这些变量可在代码中通过自动生成的基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> 属性来访问。 有关详细信息，请参阅[Using Variables in the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
> [!NOTE]  
>  变量名称区分大小写。  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 您可以选择 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 作为脚本组件的编程语言。  
  
#### <a name="edit-script-button"></a>“编辑脚本”按钮  
 **编辑脚本**按钮打开[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 在其中编写自定义脚本。 有关详细信息，请参阅[编码和调试脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>脚本转换编辑器的“连接管理器”页  
 上**连接管理器**页**脚本转换编辑器**，添加和删除你想要使用自定义脚本中的连接管理器。 通常，创建源或目标组件时需要引用连接管理器。  
  
 在代码中将生成的项目中基于此元数据， **ComponentWrapper**项目项包含**连接**为每个所选的连接管理器都有一个类型化访问器属性的集合类。 每个类型化取值函数属性的名称都与连接管理器本身的名称相同，该属性将返回对作为 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> 实例的连接管理器的引用。 例如，如果你已添加名为的连接管理器`MyADONETConnection`上**连接管理器**页的编辑器中，你可以获得对引用连接管理器在脚本中使用下面的代码：  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 有关详细信息，请参阅[连接到脚本组件中的数据源](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [编码和调试脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

