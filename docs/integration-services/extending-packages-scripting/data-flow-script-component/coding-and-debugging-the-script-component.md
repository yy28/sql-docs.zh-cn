---
title: 脚本组件的编码和调试 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c4b3337be486123545a187337949da1c160343ad
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286544"
---
# <a name="coding-and-debugging-the-script-component"></a>脚本组件的编码和调试

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中，脚本组件具有两种模式：元数据设计模式和代码设计模式。 打开“脚本转换编辑器”后，组件将进入元数据设计模式，你可以在该模式下配置元数据并设置组件属性  。 在元数据设计模式下，设置脚本组件的属性并配置输入和输出后，可以切换到代码设计模式，以编写自定义脚本。 有关元数据设计模式和代码设计模式的详细信息，请参阅[在脚本组件编辑器中配置脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
## <a name="writing-the-script-in-code-design-mode"></a>在代码设计模式下编写脚本  
  
### <a name="script-component-development-environment"></a>脚本组件开发环境  
 若要编写脚本，请在“脚本转换编辑器”的“脚本”页中，单击“编辑脚本”以打开 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE    。 VSTA IDE 包含 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET 环境的所有标准功能，如具有颜色编码的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 编辑器、IntelliSense 和对象浏览器。  
  
 脚本代码以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 编写。 在“脚本转换编辑器”中设置 ScriptLanguage 属性可指定脚本语言   。 如果您倾向于使用其他编程语言，则可以用您选择的语言开发自定义程序集，然后通过脚本组件中的代码调用其功能。  
  
 您在脚本组件中创建的脚本存储在包定义中。 由于没有单独的脚本文件， 因此，使用脚本组件不会影响包部署。  
  
> [!NOTE]  
>  设计包时，脚本代码将临时写入项目文件。 由于在文件中存储敏感信息存在潜在的安全风险，因此建议您不要在脚本代码中包含敏感信息，如密码。  
  
 默认情况下，Option Strict 在 IDE 中处于禁用状态  。  
  
### <a name="script-component-project-structure"></a>脚本组件项目结构  
 脚本组件的功能在于它可生成基础结构代码，从而减少您必须编写的代码的数量。 此功能依赖于这样一个事实：输入和输出及其列和属性都是事先固定且已知的。 因此，您对组件的元数据所做的任何后续更改都可能会使已编写的代码无效。 这将在包的执行过程中导致编译错误。  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>脚本组件项目中的项目项和类  
 切换到代码设计模式后，VSTA IDE 将打开并显示 ScriptMain 项目项  。 ScriptMain 项目项包含可编辑的 ScriptMain 类，该类用作脚本的入口点，你可在其中编写代码   。 该类中的代码元素根据您选择的脚本任务编程语言而有所不同。  
  
 脚本项目包含两个自动生成的附加只读项目项：  
  
-   ComponentWrapper 项目项包含三个类  ：  
  
    -   UserComponent 类，继承自 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>，包含你将用于处理数据和与包进行交互的方法和属性  。 ScriptMain 类继承自 UserComponent 类   。  
  
    -   Connections 集合类，包含对在“脚本转换编辑器”的“连接管理器”页上选择的连接的引用  。  
  
    -   Variables 集合类，包含对一些变量的引用，这些变量是在“脚本转换编辑器”的“脚本”页上的 ReadOnlyVariable 和 ReadWriteVariables 属性中输入的      。  
  
-   BufferWrapper 项目项，包含从每个输入和输出的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 继承的类，这些输入和输出是在“脚本转换编辑器”的“输入和输出”页上配置的    。 其中每个类都包含与已配置的输入和输出列对应的类型化取值函数属性以及包含这些列的数据流缓冲区。  
  
 有关如何使用这些对象、方法和属性的信息，请参阅[了解脚本组件对象模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)。 有关如何在特定类型的脚本组件中使用这些类的方法和属性的信息，请参阅[其他脚本组件示例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)一节。 该示例主题还包含完整的代码示例。  
  
 将脚本组件配置为转换时，ScriptMain 项目项将包含下列自动生成的代码  。 该代码模板还提供脚本组件的概览以及有关如何检索和操作 SSIS 对象（如变量、事件和连接）的其他信息。  
  
```vb  
' Microsoft SQL Server Integration Services Script Component  
' Write scripts using Microsoft Visual Basic 2008.  
' ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _  
<CLSCompliant(False)> _  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub PreExecute()  
        MyBase.PreExecute()  
        '  
        ' Add your code here for preprocessing or remove if not needed  
        '  
    End Sub  
  
    Public Overrides Sub PostExecute()  
        MyBase.PostExecute()  
        '  
        ' Add your code here for postprocessing or remove if not needed  
        ' You can set read/write variables here, for example:  
        ' Me.Variables.MyIntVar = 100  
        '  
    End Sub  
  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
        '  
        ' Add your code here  
        '  
    End Sub  
  
End Class  
```  
  
```csharp  
/* Microsoft SQL Server Integration Services user script component  
*  Write scripts using Microsoft Visual C# 2008.  
*  ScriptMain is the entry point class of the script.*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]  
public class ScriptMain : UserComponent  
{  
  
    public override void PreExecute()  
    {  
        base.PreExecute();  
        /*  
          Add your code here for preprocessing or remove if not needed  
        */  
    }  
  
    public override void PostExecute()  
    {  
        base.PostExecute();  
        /*  
          Add your code here for postprocessing or remove if not needed  
          You can set read/write variables here, for example:  
          Variables.MyIntVar = 100  
        */  
    }  
  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
        /*  
          Add your code here  
        */  
    }  
  
}  
```  
  
#### <a name="additional-project-items-in-the-script-component-project"></a>脚本组件项目中的其他项目项  
 脚本组件项目可包含默认的 ScriptMain 项以外的其他项  。 您可以向项目中添加类、模块、代码文件和文件夹，并使用文件夹来组织项组。  
  
 您添加的所有项在包中都将持久化。  
  
#### <a name="references-in-the-script-component-project"></a>脚本组件项目中的引用  
 在“项目资源管理器”中右键单击脚本任务项目，然后单击“添加引用”，可以添加对托管程序集的引用   。 有关详细信息，请参阅[引用脚本解决方案中的其他程序集](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)。  
  
> [!NOTE]  
>  可以在“类视图”或“项目资源管理器”中查看 VSTA IDE 中的项目引用   。 这些窗口都可以从“视图”菜单中打开  。 可以从“项目”菜单、“项目资源管理器”或“类视图”添加新引用    。  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>与脚本组件中的包进行交互  
 您在脚本组件中编写的自定义脚本可通过自动生成的基类中的强类型取值函数来访问和使用包含包中的变量和连接管理器。 但是，若要使这些变量和连接管理器可用于您的脚本，您必须先对它们进行配置，然后才可进入代码设计模式。 还可以从脚本组件代码引发事件并执行日志记录。  
  
 脚本组件项目中自动生成的项目项可提供以下用于与包进行交互的对象、方法和属性。  
  
|包的功能|访问方法|  
|---------------------|-------------------|  
|变量|使用 ComponentWrapper 项目项的 Variables 集合类中的命名取值函数属性和类型化取值函数属性，这些属性通过 ScriptMain 类的 Variables 属性公开     。<br /><br /> PreExecute 方法仅可访问只读变量  。 **PostExecute** 方法既可访问只读变量，又可访问读/写变量。|  
|连接|使用 ComponentWrapper 项目项的 Connections 集合类中的命名取值函数属性和类型化取值函数属性，这些属性通过 ScriptMain 类的 Connections 属性公开     。|  
|事件|使用 ScriptMain 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 属性和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 接口的 Fire\<X> 方法引发事件   。|  
|日志记录|使用 ScriptMain 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法执行日志记录  。|  
  
## <a name="debugging-the-script-component"></a>调试脚本组件  
 若要调试脚本组件中的代码，请在代码中设置至少一个断点，然后关闭 VSTA IDE 以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中运行包。 当包执行进入脚本组件时，VSTA IDE 会在只读模式下重新打开并显示您的代码。 包执行到达您的断点后，您可以检查变量值，并单步执行剩余代码。  
  
> [!NOTE]  
>  如果将脚本组件作为从执行包任务运行的子包的一部分来执行，则不能调试该脚本组件。 在这些情况下，您在子包的脚本组件中设置的断点将被忽略。 您可以通过单独运行子包来正常调试子包。  
  
> [!NOTE]  
>  当调试包含多个脚本组件的包时，调试器将调试一个脚本组件。 系统可以在调试器完成调试后调试另一个脚本组件，就像在 Foreach 循环容器或 For 循环容器中那样。  
  
 还可以使用以下方法监视脚本组件的执行：  
  
-   使用 System.Windows.Forms 命名空间的 MessageBox.Show 方法中断执行并显示模式消息   。 （调试过程结束后，请删除此代码。）  
  
-   引发信息性消息、警告和错误的事件。 FireInformation、FireWarning 和 FireError 方法可在 Visual Studio“输出”窗口中显示事件说明  。 但是，FireProgress、Console.Write 和 Console.WriteLine 方法在“输出”窗口中不显示任何信息  。 FireProgress 事件的消息显示在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器的“进度”选项卡中  。 有关详细信息，请参阅[在脚本组件中引发事件](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)。  
  
-   将事件或用户定义的消息记录到已启用的日志记录提供程序中。 有关详细信息，请参阅[脚本组件中的日志记录](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)。  
  
 如果你只想检查配置为源或转换的脚本组件的输出，而不将数据保存到目标，则可以使用[行计数转换](../../../integration-services/data-flow/transformations/row-count-transformation.md)停止数据流，并向脚本组件的输出附加一个数据查看器。 有关数据查看器的信息，请参阅[调试数据流](../../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
## <a name="in-this-section"></a>本节内容  
 有关编写脚本组件代码的详细信息，请参阅本节中的下列主题。  
  
 [了解脚本组件对象模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 介绍如何使用脚本组件中可用的对象、方法和属性。  
  
 [引用脚本解决方案中的其他程序集](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 介绍如何在脚本组件中从 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 类库引用对象。  
  
 [模拟脚本组件的错误输出](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 介绍如何使用脚本组件模拟在处理期间引发错误的行的错误输出。  
  
## <a name="external-resources"></a>外部资源  
  
-   blogs.msdn.com 上的博客文章：[VSTA setup and configuration troubles for SSIS 2008 and R2 installations（针对 SSIS 2008 和 R2 安装的 VSTA 安装和配置难题）](https://go.microsoft.com/fwlink/?LinkId=215661)。  
  
## <a name="see-also"></a>另请参阅  
 [在脚本组件编辑器中配置脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
  
  
