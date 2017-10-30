---
title: "使用脚本组件创建异步转换 |Microsoft 文档"
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
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4da61e00337430a3eaef84e40f9f732a572cc45b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>使用脚本组件创建异步转换
  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的数据流中使用转换组件可以在数据从源传递到目标时修改和分析该数据。 具有同步输出的转换在每个输入行传递给该组件时对该行进行处理。 具有异步输出的转换可能需要等待才能完成其处理，直到转换已收到所有输入的行，或转换可能输出某些行之前收到所有输入的行。 本主题讨论异步转换。 如果你处理需要同步的转换，请参阅[使用脚本组件创建同步转换](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)。 同步和异步组件之间的差异的详细信息，请参阅[了解同步和异步转换](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)。  
  
 脚本组件的概述，请参阅[Extending the Data Flow with Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 脚本组件及其生成的基础结构代码可以简化自定义数据流组件的开发过程。 但是，若要了解脚本组件的工作原理，你可能发现很有用通读的步骤，你必须在开发中的自定义数据流组件[开发自定义数据流组件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)部分中，和尤其是[开发具有同步输出的自定义转换组件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)。  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>开始一个异步转换组件  
 当将脚本组件添加到数据流选项卡的[!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器中，**选择脚本组件类型**显示的对话框中，将提示您进行预配置为源、 转换或目标的组件。 在此对话框中，选择**转换**。  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>在元数据设计模式下配置异步转换组件  
 通过选择此选项来创建转换组件后，配置该组件**脚本转换编辑器**。 有关详细信息，请参阅[配置脚本组件编辑器中的脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要选择脚本组件将使用的脚本语言，请设置**ScriptLanguage**属性**脚本**页**脚本转换编辑器**对话框框。  
  
> [!NOTE]  
>  若要设置的默认脚本语言的脚本组件，使用**脚本语言**选项**常规**页**选项**对话框。 有关详细信息，请参阅 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
 数据流转换组件有一个输入并支持一个或多个输出。 配置的输入和输出的组件是必须使用在元数据设计模式下，完成的步骤之一**脚本转换编辑器**，需要在编写自定义脚本前。  
  
### <a name="configuring-input-columns"></a>配置输入列  
 使用脚本组件创建的转换组件只有一个输入。  
  
 上**输入列**页**脚本转换编辑器**，列列表显示可用列从上游组件的输出数据流中的数据。 选择要转换或传递的列。 将要就地转换的所有列标记为读/写。  
  
 有关详细信息**输入列**页**脚本转换编辑器**，请参阅[脚本转换编辑器 （; 输入列页) #41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)。  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>配置输入、输出和输出列  
 转换组件支持一个或多个输出。  
  
 通常，具有异步输出的转换有两个输出。 例如，在您对位于特定城市中的地址进行计数时，可以将地址数据传递给一个输出，同时将聚合结果发送给另一个输出。 聚合输出还需要一个新的输出列。  
  
 上**输入和输出**页**脚本转换编辑器**，你看到默认情况下，创建一个输出，但已创建任何输出列。 可以在编辑器的这一页配置下列各项：  
  
-   您可能希望创建一个或多个附加输出，如聚合结果的输出。 使用**添加输出**和**删除输出**按钮来管理异步转换组件的输出。 设置**SynchronousInputID**属性为零，以指示输出不会不只是从上游组件传递数据或在现有行和列中的位置对其进行转换的每个输出。 此设置使输出和输入异步。  
  
-   您可以为输入和输出指定一个友好名称。 脚本组件可以使用这些名称来生成类型化取值函数属性，这些属性用于在脚本中引用输入和输出。  
  
-   通常，异步转换会向数据流添加列。 当**SynchronousInputID**的输出的属性为零、，该值指示输出不只传递数据，从上游组件或转换中的现有行和列，必须添加和配置显式上输出的输出列。 输出列不必与其所映射到的输入列同名。  
  
-   您可以添加更多列来包含其他信息。 您必须编写自己的代码来向这些附加列填充数据。 有关重现标准错误输出的行为的信息，请参阅[脚本组件为模拟错误输出](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 有关详细信息**输入和输出**页**脚本转换编辑器**，请参阅[脚本转换编辑器 （; 输入和输出页) #41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>添加变量  
 如果有任何现有的变量在脚本中你要使用其值，你可以添加它们在 ReadOnlyVariables 和 ReadWriteVariables 属性字段中在**脚本**页**脚本转换编辑器**.  
  
 在属性字段中添加多个变量时，请用逗号将变量名隔开。 此外可以选择多个变量，通过单击省略号 (**...**) 按钮旁边**ReadOnlyVariables**和**ReadWriteVariables**属性字段，然后选择中的变量**选择变量**对话框。  
  
 有关如何使用脚本组件中使用变量的常规信息，请参阅[Using Variables in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 有关详细信息**脚本**页**脚本转换编辑器**，请参阅[脚本转换编辑器 &#40;脚本页 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>在代码设计模式下编写异步转换组件脚本  
 为组件配置完所有元数据后，可以编写自定义脚本。 在**脚本转换编辑器**上**脚本**页上，单击**编辑脚本**以打开[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE你可在其中添加自定义脚本。 你使用的脚本语言取决于你是选择还是[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual C# 作为的脚本语言**ScriptLanguage**属性**脚本**页。  
  
 适用于所有类型的使用脚本组件创建的组件的重要信息，请参阅[编码和调试脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自动生成的代码  
 当在创建并配置可编辑的转换组件后打开 VSTA IDE **ScriptMain**使用存根在代码编辑器中显示为 ProcessInputRow 和 CreateNewOutputRows 方法的类。 ScriptMain 类是其中你将编写自定义代码，并且 ProcessInputRow 是转换组件中最重要的方法。 **CreateNewOutputRows**方法更通常使用源组件相当于异步转换可两个组件必须创建自己的输出行中。  
  
 如果打开 VSTA**项目资源管理器**窗口中，你可以看到，脚本组件也具有生成只读**BufferWrapper**和**ComponentWrapper**项目项. ScriptMain 类继承自中的 UserComponent 类**ComponentWrapper**项目项。  
  
 在运行时，数据流引擎调用 PrimeOutput 方法**UserComponent**类，该类会重写<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父类。 PrimeOutput 方法反过来调用 CreateNewOutputRows 方法。  
  
 数据流引擎接下来，在 UserComponent 类中，这会重写的 ProcessInput 方法时，将调用<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父类。 反过来，ProcessInput 方法循环遍历输入缓冲区中的行，并为每个行调用 ProcessInputRow 方法一次。  
  
### <a name="writing-your-custom-code"></a>编写自定义代码  
 若要完成创建自定义异步转换组件，必须使用重写的 ProcessInputRow 方法以处理输入缓冲区中的每一行中的数据。 由于输出与输入不同步，因此您必须向输出显式写入数据行。  
  
 在异步转换中，你可以使用 AddRow 方法以将行添加到在 ProcessInputRow 或 ProcessInput 方法内从根据输出。 无需使用 CreateNewOutputRows 方法。 如果你正在写入特定输出结果，如聚合结果的单个行，你可以使用 CreateNewOutputRows 方法中，事先创建输出行，在处理所有输入的行后填充其值。 但是它不用于创建多个行在 CreateNewOutputRows 方法中，因为脚本组件仅能让您使用的输入或输出中的当前行。 CreateNewOutputRows 方法是源组件中更重要其中不有任何要处理的输入的行。  
  
 你可能还想要重写 ProcessInput 方法本身，以便您可以执行其他初步或最后一个处理之前或之后循环访问输入缓冲区，并为每个行调用 ProcessInputRow。 例如，其中一个此主题中的代码示例替代 ProcessInput 才能计为 ProcessInputRow 循环访问行的特定城市中的地址数**。** 在处理所有行之后，该示例将写入第二个输出的汇总值。 示例完成 ProcessInput 中的输出，因为输出缓冲区仅调用 PostExecute 时不再可用。  
  
 具体取决于你的要求，你可能还想要在 ScriptMain 类来执行任何基本或最后一个处理中提供的 PreExecute 和 PostExecute 方法中编写脚本。  
  
> [!NOTE]  
>  如果你正在开发自定义数据流组件从零开始，它将会重写到缓存引用到输出缓冲区的 PrimeOutput 方法，以便可以更高版本添加到的缓冲区的行数据十分重要。 在脚本组件中，这是不必要由于你有一个自动生成的类，表示在每个输出缓冲区**BufferWrapper**项目项。  
  
## <a name="example"></a>示例  
 此示例演示了需要在 ScriptMain 类来创建异步转换组件的自定义代码。  
  
> [!NOTE]  
>  这些示例使用**Person.Address**表中**AdventureWorks**示例数据库并将传递其第一个和第四个列， **intAddressID**和**nvarchar (30) 城市**列，该数据工作流中的。 在本节中，在源、转换和目标示例中使用相同的数据。 每个示例的其他前提条件和假设都记录在文档中。  
  
 此示例演示具有两个输出的异步转换组件。 此转换传递**AddressID**和**城市**到一个输出，而它对位于特定城市 （Redmond，Washington，美国） 的地址数进行计数，然后输出列到第二个输出的结果值。  
  
 如果要运行此示例代码，必须按照如下方式配置包和组件：  
  
1.  向数据流设计器图面添加新的脚本组件并将其配置为转换。  
  
2.  在设计器中将源或另一转换的输出连接到新转换组件。 此输出应提供从数据**Person.Address**表**AdventureWorks**包含的示例数据库至少**AddressID**和**城市**列。  
  
3.  打开**脚本转换编辑器**。 上**输入列**页上，选择**AddressID**和**城市**列。  
  
4.  上**输入和输出**页上，添加和配置**AddressID**和**城市**输出上的第一个输出列。 添加另一个输出，然后向第二个输出添加汇总值的输出列。 将第一个输出的 SynchronousInputID 属性设置为 0，因为此示例显式将每个输入行复制到第一个输出中。 新创建的输出的 SynchronousInputID 属性已经设置为 0。  
  
5.  重命名输入、输出和新输出列，使其名称更具说明性。 该示例使用**MyAddressInput**作为名称的输入， **MyAddressOutput**和**MySummaryOutput**的输出和**MyRedmondCount**上第二个输出的输出列。  
  
6.  上**脚本**页上，单击**编辑脚本**和输入遵循的脚本。 然后关闭脚本开发环境和**脚本转换编辑器**。  
  
7.  创建和配置要求的第一个输出的目标组件**AddressID**和**城市**列，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标，地址或示例目标组件所示[使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 然后将连接的转换时，第一个输出**MyAddressOutput**，到目标组件。 你可以通过运行以下命令，创建的目标表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**数据库：  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  为第二个输出创建和配置另一个目标组件。 第二个输出的转换，然后连接**MySummaryOutput**，到目标组件。 由于第二个输出写入只带有一个值的一行，因此可以轻松对目标配置一个连接到只含一列的新文件的平面文件连接管理器。 在本示例中，此目标列的名称为**MyRedmondCount**。  
  
9. 运行该示例。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Private myRedmondAddressCount As Integer  
  
    Public Overrides Sub CreateNewOutputRows()  
  
        MySummaryOutputBuffer.AddRow()  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInput(ByVal Buffer As MyAddressInputBuffer)  
  
        While Buffer.NextRow()  
            MyAddressInput_ProcessInputRow(Buffer)  
        End While  
  
        If Buffer.EndOfRowset Then  
            MyAddressOutputBuffer.SetEndOfRowset()  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount  
            MySummaryOutputBuffer.SetEndOfRowset()  
        End If  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With MyAddressOutputBuffer  
            .AddRow()  
            .AddressID = Row.AddressID  
            .City = Row.City  
        End With  
  
        If Row.City.ToUpper = "REDMOND" Then  
            myRedmondAddressCount += 1  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    private int myRedmondAddressCount;  
  
    public override void CreateNewOutputRows()  
    {  
  
        MySummaryOutputBuffer.AddRow();  
  
    }  
  
    public override void MyAddressInput_ProcessInput(MyAddressInputBuffer Buffer)  
    {  
  
        while (Buffer.NextRow())  
        {  
            MyAddressInput_ProcessInputRow(Buffer);  
        }  
  
        if (Buffer.EndOfRowset())  
        {  
            MyAddressOutputBuffer.SetEndOfRowset();  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount;  
            MySummaryOutputBuffer.SetEndOfRowset();  
        }  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            MyAddressOutputBuffer.AddRow();  
            MyAddressOutputBuffer.AddressID = Row.AddressID;  
            MyAddressOutputBuffer.City = Row.City;  
        }  
  
        if (Row.City.ToUpper() == "REDMOND")  
        {  
            myRedmondAddressCount += 1;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [了解同步和异步转换](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [使用脚本组件创建同步转换](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [开发具有异步输出的自定义转换组件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
