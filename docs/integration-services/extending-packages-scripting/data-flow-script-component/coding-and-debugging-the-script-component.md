---
title: "编码和调试脚本组件 |Microsoft 文档"
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
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
caps.latest.revision: 66
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ff6c9814547a83439717f8a88d3bd52be80c4ca5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="coding-and-debugging-the-script-component"></a>脚本组件的编码和调试
  在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中，脚本组件具有两种模式：元数据设计模式和代码设计模式。 当你打开**脚本转换编辑器**，组件会输入元数据设计模式中，在其中配置元数据和设置组件属性。 在元数据设计模式下，设置脚本组件的属性并配置输入和输出后，可以切换到代码设计模式，以编写自定义脚本。 有关设计模式中元数据和代码设计模式的详细信息，请参阅[配置脚本组件编辑器中的脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
## <a name="writing-the-script-in-code-design-mode"></a>在代码设计模式下编写脚本  
  
### <a name="script-component-development-environment"></a>脚本组件开发环境  
 若要编写脚本，请单击**编辑脚本**上**脚本**页**脚本转换编辑器**以打开[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE。 VSTA IDE 包含 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET 环境的所有标准功能，如具有颜色编码的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 编辑器、IntelliSense 和对象浏览器。  
  
 脚本代码以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 编写。 通过设置指定的脚本语言**ScriptLanguage**中的属性**脚本转换编辑器**。 如果您倾向于使用其他编程语言，则可以用您选择的语言开发自定义程序集，然后通过脚本组件中的代码调用其功能。  
  
 您在脚本组件中创建的脚本存储在包定义中。 由于没有单独的脚本文件， 因此，使用脚本组件不会影响包部署。  
  
> [!NOTE]  
>  设计包时，脚本代码将临时写入项目文件。 由于在文件中存储敏感信息存在潜在的安全风险，因此建议您不要在脚本代码中包含敏感信息，如密码。  
  
 默认情况下， **Option Strict**在 IDE 中禁用。  
  
### <a name="script-component-project-structure"></a>脚本组件项目结构  
 脚本组件的功能在于它可生成基础结构代码，从而减少您必须编写的代码的数量。 此功能依赖于这样一个事实：输入和输出及其列和属性都是事先固定且已知的。 因此，您对组件的元数据所做的任何后续更改都可能会使已编写的代码无效。 这将在包的执行过程中导致编译错误。  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>脚本组件项目中的项目项和类  
 当你切换到代码设计模式时，将打开 VSTA IDE，并显示**ScriptMain**项目项。 **ScriptMain**项目项包含可编辑**ScriptMain**类，后者相当于入口点脚本和这是你在其中编写代码。 该类中的代码元素根据您选择的脚本任务编程语言而有所不同。  
  
 脚本项目包含两个自动生成的附加只读项目项：  
  
-   **ComponentWrapper**项目项包含三个类：  
  
    -   **UserComponent**类，该类继承自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>和包含的方法和属性将用于处理数据并与包进行交互。 **ScriptMain**类继承自**UserComponent**类。  
  
    -   A**连接**包含对的脚本转换编辑器中的连接管理器页上选中的连接引用的集合类。  
  
    -   A**变量**包含对输入中的变量的引用的集合类**ReadOnlyVariable**和**ReadWriteVariables**属性**脚本**页**脚本转换编辑器**。  
  
-   **BufferWrapper**项目项包含一个类继承自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>为每个输入和输出上配置**输入和输出**页**脚本转换编辑器**。 其中每个类都包含与已配置的输入和输出列对应的类型化取值函数属性以及包含这些列的数据流缓冲区。  
  
 有关如何使用这些对象、 方法和属性的信息，请参阅[了解脚本组件对象模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)。 有关如何在特定类型的脚本组件中使用的方法和属性，这些类的信息，请参阅明[Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。 该示例主题还包含完整的代码示例。  
  
 当你将脚本组件配置为一个转换， **ScriptMain**项目项包含以下自动生成代码。 该代码模板还提供脚本组件的概览以及有关如何检索和操作 SSIS 对象（如变量、事件和连接）的其他信息。  
  
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
 脚本组件项目可以包含非默认的项**ScriptMain**项。 您可以向项目中添加类、模块、代码文件和文件夹，并使用文件夹来组织项组。  
  
 您添加的所有项在包中都将持久化。  
  
#### <a name="references-in-the-script-component-project"></a>脚本组件项目中的引用  
 可以通过右键单击中的脚本任务项目添加到托管程序集的引用**项目资源管理器**，然后单击**添加引用**。 有关详细信息，请参阅[脚本解决方案中引用其他程序集](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)。  
  
> [!NOTE]  
>  你可以在 VSTA IDE 中查看项目引用**类视图**或**项目资源管理器**。 打开这些窗口阻止任一**视图**菜单。 你可以添加中的新引用**项目**菜单上，从**项目资源管理器**，或从**类视图**。  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>与脚本组件中的包进行交互  
 您在脚本组件中编写的自定义脚本可通过自动生成的基类中的强类型取值函数来访问和使用包含包中的变量和连接管理器。 但是，若要使这些变量和连接管理器可用于您的脚本，您必须先对它们进行配置，然后才可进入代码设计模式。 还可以从脚本组件代码引发事件并执行日志记录。  
  
 脚本组件项目中自动生成的项目项可提供以下用于与包进行交互的对象、方法和属性。  
  
|包的功能|访问方法|  
|---------------------|-------------------|  
|变量|使用中的命名和类型化访问器属性**变量**中的集合类**ComponentWrapper**项目项，通过公开**变量**属性**ScriptMain**类。<br /><br /> **PreExecute**方法可以访问仅只读变量。 **PostExecute**方法可以访问同时表示两者只读的读/写变量。|  
|连接|使用中的命名和类型化访问器属性**连接**中的集合类**ComponentWrapper**项目项，通过公开**连接**属性**ScriptMain**类。|  
|事件|引发事件，通过使用<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>属性**ScriptMain**类和**激发\<X >**方法<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>接口。|  
|日志记录|通过使用执行日志记录<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>方法**ScriptMain**类。|  
  
## <a name="debugging-the-script-component"></a>调试脚本组件  
 若要调试脚本组件中的代码，请在代码中设置至少一个断点，然后关闭 VSTA IDE 以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中运行包。 当包执行进入脚本组件时，VSTA IDE 会在只读模式下重新打开并显示您的代码。 包执行到达您的断点后，您可以检查变量值，并单步执行剩余代码。  
  
> [!NOTE]  
>  如果将脚本组件作为从执行包任务运行的子包的一部分来执行，则不能调试该脚本组件。 在这些情况下，您在子包的脚本组件中设置的断点将被忽略。 您可以通过单独运行子包来正常调试子包。  
  
> [!NOTE]  
>  当调试包含多个脚本组件的包时，调试器将调试一个脚本组件。 系统可以在调试器完成调试后调试另一个脚本组件，就像在 Foreach 循环容器或 For 循环容器中那样。  
  
 还可以使用以下方法监视脚本组件的执行：  
  
-   中断执行，并通过使用显示模式消息**MessageBox.Show**中的方法**System.Windows.Forms**命名空间。 （调试过程结束后，请删除此代码。）  
  
-   引发信息性消息、警告和错误的事件。 FireInformation、 FireWarning 和 FireError 方法在 Visual Studio 中显示事件描述**输出**窗口。 但是，FireProgress 方法、 Console.Write 方法和 Console.WriteLine 方法不显示任何信息在**输出**窗口。 从 FireProgress 事件的消息将显示在**进度**选项卡[!INCLUDE[ssIS](../../../includes/ssis-md.md)]设计器。 有关详细信息，请参阅[在脚本组件中引发事件](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)。  
  
-   将事件或用户定义的消息记录到已启用的日志记录提供程序中。 有关详细信息，请参阅[脚本组件中的日志记录](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)。  
  
 如果你只想要检查配置作为源或转换，而无需将数据保存到目标，脚本组件的输出可能会停止与数据流[Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md)并将数据查看器附加到脚本组件的输出。 有关数据查看器的信息，请参阅[Debugging Data Flow](../../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
## <a name="in-this-section"></a>本節內容  
 有关编写脚本组件代码的详细信息，请参阅本节中的下列主题。  
  
 [了解脚本组件对象模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 介绍如何使用脚本组件中可用的对象、方法和属性。  
  
 [引用在脚本的解决方案中的其他程序集](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 介绍如何在脚本组件中从 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 类库引用对象。  
  
 [为脚本组件模拟错误输出](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 介绍如何使用脚本组件模拟在处理期间引发错误的行的错误输出。  
  
## <a name="external-resources"></a>外部资源  
  
-   博客文章[SSIS 2008 和 R2 安装的 VSTA 安装和配置问题](http://go.microsoft.com/fwlink/?LinkId=215661)，blogs.msdn.com 上的。  
  
## <a name="see-also"></a>另请参阅  
 [配置脚本组件编辑器中的脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
  
  

