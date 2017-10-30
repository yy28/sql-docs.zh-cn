---
title: "使用脚本组件创建同步转换 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
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
helpviewer_keywords:
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d4a507c31f77449aba7eb884c39bf68c7c78581
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>使用脚本组件创建同步转换
  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的数据流中使用转换组件可以在数据从源传递到目标时修改和分析该数据。 具有同步输出的转换在每个输入行传递给该组件时对该行进行处理。 具有异步输出的转换在等到接收所有输入行之后才能完成处理。 本主题讨论同步转换。 有关异步转换的信息，请参阅[使用脚本组件创建异步转换](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。 有关同步和异步组件之间的差异的详细信息，请参阅[了解同步和异步转换](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)。  
  
 脚本组件的概述，请参阅[Extending the Data Flow with Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 脚本组件及其生成的基础结构代码可以大大简化自定义数据流组件的开发过程。 但是，若要了解脚本组件的工作原理，你可能发现很有用读取你必须中上进行开发自定义数据流组件的部分中执行的步骤[开发自定义数据流组件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)，尤其是[开发具有同步输出的自定义转换组件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)。  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>开始一个同步转换组件  
 当将脚本组件添加到的数据流窗格[!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器中，**选择脚本组件类型**对话框将打开，提示你选择的源、 目标或转换组件类型。 在此对话框中，选择**转换**。  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>在元数据设计模式下配置同步转换组件  
 通过选择此选项来创建转换组件后，配置该组件**脚本转换编辑器**。 有关详细信息，请参阅[配置脚本组件编辑器中的脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要设置的脚本组件的脚本语言，你可以设置**ScriptLanguage**属性**脚本**页**脚本转换编辑器**。  
  
> [!NOTE]  
>  若要设置的默认脚本语言的脚本组件，使用**脚本语言**选项**常规**页**选项**对话框。 有关详细信息，请参阅[常规页](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
 数据流转换组件具有一个输入，并支持一个或多个输出。 为该组件是必须使用在元数据设计模式下，完成的步骤之一配置的输入和输出**脚本转换编辑器**，需要在编写自定义脚本前。  
  
### <a name="configuring-input-columns"></a>配置输入列  
 转换组件具有一个输入。  
  
 上**输入列**页**脚本转换编辑器**列列表显示可用列从上游组件的输出数据流中的数据。 选择要转换或传递的列。 将要就地转换的所有列标记为读/写。  
  
 有关详细信息**输入列**页**脚本转换编辑器**，请参阅[脚本转换编辑器 （; 输入列页) #41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)。  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>配置输入、输出和输出列  
 转换组件支持一个或多个输出。  
  
 上**输入和输出**页**脚本转换编辑器**，你可以看到已创建一个输出，但输出结果的任何列。 在编辑器的这一页，可能需要或希望配置以下各项。  
  
-   创建一个或多个附加输出，如包含意外值的行的模拟错误输出。 使用**添加输出**和**删除输出**按钮来管理同步转换组件的输出。 所有输入行都定向到所有可用输出，除非您表示希望将每一行重定向到一个输出或其他输出。 指示你想要通过指定的非零整数值将行重定向**ExclusionGroup**上输出的属性。 特定的整数值中输入**ExclusionGroup**来标识输出并不重要，但你必须指定组的输出的一致地使用相同的整数。  
  
    > [!NOTE]  
    >  你还可以使用非零**ExclusionGroup**与单个输出时不希望输出所有行的属性值。 但是，在这种情况下，你必须明确地调用**DirectRowTo\<outputbuffer >**为你想要将发送到输出的每一行的方法。  
  
-   为输入和输出指定一个更具说明性的名称。 脚本组件可以使用这些名称来生成类型化取值函数属性，这些属性用于在脚本中引用输入和输出。  
  
-   对于同步转换，将列保持原样。 通常，同步转换不会向数据流添加列。 会在缓冲区中就地修改数据，然后将缓冲区传递到数据流的下一个组件中。 如果是这种情况，您不需要对转换的输出显式添加和配置输出列。 输出显示在编辑器中，并且不包含任何显式定义的列。  
  
-   向行级错误的模拟错误输出添加新列。 多个在相同的输出通常**ExclusionGroup**具有相同的输出列集。 但是，如果要创建模拟的错误输出，则可能要添加多个列来包含错误信息。 有关如何数据流引擎的信息处理错误行，请参阅[数据流组件中使用错误输出](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)。 请注意，在脚本组件中，必须编写您自己的代码以便使用适当的错误信息填充这些附加列。 有关详细信息，请参阅[脚本组件为模拟错误输出](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 有关详细信息**输入和输出**页**脚本转换编辑器**，请参阅[脚本转换编辑器 （; 输入和输出页) #41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>添加变量  
 如果你想要在脚本中使用现有的变量，则可以添加在**ReadOnlyVariables**和**ReadWriteVariables**属性字段上**脚本**页**脚本转换编辑器**。  
  
 在属性字段中添加多个变量时，请用逗号将变量名隔开。 此外可以选择多个变量，通过单击省略号 (**...**) 按钮旁边**ReadOnlyVariables**和**ReadWriteVariables**属性字段，然后选择中的变量**选择变量**对话框。  
  
 有关如何使用脚本组件中使用变量的常规信息，请参阅[Using Variables in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 有关详细信息**脚本**页**脚本转换编辑器**，请参阅[脚本转换编辑器 &#40;脚本页 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>在代码设计模式下编写同步转换组件脚本  
 为组件配置完元数据后，可以编写自定义脚本。 在**脚本转换编辑器**上**脚本**页上，单击**编辑脚本**以打开[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE你可在其中添加自定义脚本。 你使用的脚本语言取决于你是选择还是[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual C# 作为的脚本语言**ScriptLanguage**属性**脚本**页。  
  
 适用于所有类型的使用脚本组件创建的组件的重要信息，请参阅[编码和调试脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自动生成的代码  
 当你打开 VSTA IDE 后你创建和配置转换组件，可编辑**ScriptMain**类将出现在代码编辑器中使用存根出于**ProcessInputRow**方法。 **ScriptMain**类是你将在其中编写自定义代码，和**ProcessInputRow**是转换组件中最重要的方法。  
  
 如果你打开**项目资源管理器**在 VSTA 中的窗口中，你可以看到，脚本组件也具有生成只读**BufferWrapper**和**ComponentWrapper**项目项。 **ScriptMain**类继承自**UserComponent**类**ComponentWrapper**项目项。  
  
 在运行时，数据流引擎调用**ProcessInput**中的方法**UserComponent**类，该类会重写<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父类。 **ProcessInput**方法反过来循环访问的输入的缓冲区和调用中的行**ProcessInputRow**方法一次为每个行。  
  
### <a name="writing-your-custom-code"></a>编写自定义代码  
 具有同步传输的转换组件是要编写的所有数据流组件中最简单的部分。 例如，本主题中稍后演示的单个输出示例包含以下自定义代码：  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 若要完成创建自定义同步转换组件，请使用重写**ProcessInputRow**方法转换输入缓冲区中的每个行中的数据。 缓冲区写满后，数据流引擎会将此缓冲区传递给数据流中的下一个组件。  
  
 具体取决于你的要求，你可能还想要编写脚本**PreExecute**和**PostExecute**中可用方法**ScriptMain**类中，以执行初步或最后一个处理。  
  
### <a name="working-with-multiple-outputs"></a>使用多个输出  
 将输入行定向到两个或多个可能的输出中的一个输出时所需的自定义代码比之前讨论的单个输出方案所需的代码要少得多。 例如，本主题中稍后演示的两个输出示例包含以下自定义代码：  
  
```vb  
Row.City = UCase(Row.City)  
If Row.City = "REDMOND" Then  
    Row.DirectRowToMyRedmondAddresses()  
Else  
    Row.DirectRowToMyOtherAddresses()  
End If  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
if (Row.City=="REDMOND")  
{  
    Row.DirectRowToMyRedmondAddresses();  
}  
else  
{  
    Row.DirectRowToMyOtherAddresses();  
}  
```  
  
 在此示例中，脚本组件生成**DirectRowTo\<OutputBufferX >**方法，基于你配置的输出名称。 您可以使用类似的代码将错误行定向到模拟的错误输出。  
  
## <a name="examples"></a>示例  
 此处的示例演示自定义代码中所需**ScriptMain**类创建同步转换组件。  
  
> [!NOTE]  
>  这些示例使用**Person.Address**表中**AdventureWorks**示例数据库并将传递其第一个和第四个列， **intAddressID**和**nvarchar (30) 城市**列，该数据工作流中的。 在本节中，在源、转换和目标示例中使用相同的数据。 每个示例的其他前提条件和假设都记录在文档中。  
  
### <a name="single-output-synchronous-transformation-example"></a>单个输出同步转换示例  
 此示例演示具有单个输出的同步转换组件。 此转换传递**AddressID**列并将转换**城市**为大写形式的列。  
  
 如果要运行此示例代码，必须按照如下方式配置包和组件：  
  
1.  向数据流设计器图面添加新的脚本组件并将其配置为转换。  
  
2.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中将源或另一转换的输出连接到新转换组件。 此输出应提供从数据**Person.Address**表**AdventureWorks**包含的示例数据库**AddressID**和**城市**列。  
  
3.  打开**脚本转换编辑器**。 上**输入列**页上，选择**AddressID**和**城市**列。 标记**城市**作为读/写列。  
  
4.  上**输入和输出**页上，重命名输入，输出更具描述性的名称，如**MyAddressInput**和**MyAddressOutput**。 请注意， **SynchronousInputID**输出的对应于**ID**的输入。 因此，您不需要添加和配置输出列。  
  
5.  上**脚本**页上，单击**编辑脚本**和输入遵循的脚本。 然后关闭脚本开发环境和**脚本转换编辑器**。  
  
6.  创建和配置要求的目标组件**AddressID**和**城市**列，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标，地址或示例目标组件所示[使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 然后，将转换的输出连接到目标组件。 你可以通过运行以下命令，创建的目标表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**数据库：  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  运行该示例。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
    }  
  
}  
```  
  
### <a name="two-output-synchronous-transformation-example"></a>两个输出同步转换示例  
 此示例演示具有两个输出的同步转换组件。 此转换传递**AddressID**列并将转换**城市**为大写形式的列。 如果城市名为 Redmond，则将行定向到一个输出；将所有其他行定向到另一个输出。  
  
 如果要运行此示例代码，必须按照如下方式配置包和组件：  
  
1.  向数据流设计器图面添加新的脚本组件并将其配置为转换。  
  
2.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中将源或另一转换的输出连接到新转换组件。 此输出应提供从数据**Person.Address**表**AdventureWorks**包含的示例数据库至少**AddressID**和**城市**列。  
  
3.  打开**脚本转换编辑器**。 上**输入列**页上，选择**AddressID**和**城市**列。 标记**城市**作为读/写列。  
  
4.  上**输入和输出**页上，创建第二个输出。 添加新的输出之后，请确保你设置其**SynchronousInputID**到**ID**的输入。 已对第一个输出设置此属性，该输出是默认创建的。 对于每个输出中，设置**ExclusionGroup**属性相同的非零值，以指示您将拆分之间两个互相排斥的输出的输入的行。 无需向输出添加任何输出列。  
  
5.  重命名的输入和输出更具描述性的名称，例如**MyAddressInput**， **MyRedmondAddresses**，和**MyOtherAddresses**。  
  
6.  上**脚本**页上，单击**编辑脚本**和输入遵循的脚本。 然后关闭脚本开发环境和**脚本转换编辑器**。  
  
7.  创建和配置预期的两个目标组件**AddressID**和**城市**列，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标、 平面文件目标或示例目标组件所示[使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 然后，将转换的每个输出连接到任一目标组件。 你可以通过运行创建目标表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令类似于 （使用唯一表名称） 中的以下**AdventureWorks**数据库：  
  
    ```sql
    CREATE TABLE [Person].[Address2](  
        [AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL  
    ```  
  
8.  运行该示例。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
        If Row.City = "REDMOND" Then  
            Row.DirectRowToMyRedmondAddresses()  
        Else  
            Row.DirectRowToMyOtherAddresses()  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
        if (Row.City == "REDMOND")  
        {  
            Row.DirectRowToMyRedmondAddresses();  
        }  
        else  
        {  
            Row.DirectRowToMyOtherAddresses();  
        }  
  
    }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [了解同步和异步转换](~/integration-services/understanding-synchronous-and-asynchronous-transformations.md   
 [使用脚本组件创建异步转换](~/integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md   
 [开发具有同步输出的自定义转换组件](~/integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md  
  
  



