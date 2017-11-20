---
title: "了解脚本组件对象模型 |Microsoft 文档"
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
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 09de00344fe94087b6287b07c4b1ffe933d27b7c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="understanding-the-script-component-object-model"></a>了解脚本组件对象模型
  中所述[编码和调试脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)，脚本组件项目包含三个项目项：  
  
1.  **ScriptMain**项，其中包含**ScriptMain**在其中编写代码的类。 **ScriptMain**类继承自**UserComponent**类。  
  
2.  **ComponentWrapper**项，其中包含**UserComponent**类的实例<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>，其中包含的方法和属性将用于处理数据并与包进行交互。 **ComponentWrapper**项还包含**连接**和**变量**集合类。  
  
3.  **BufferWrapper**项，其中包含继承自的类<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>为每个列每个输入和输出，和类型化的属性。  
  
 在中编写代码**ScriptMain**项，将使用对象、 方法和本主题中讨论的属性。 每个组件不会用到此处列出的所有方法；但用到的方法都会按照此处所示的顺序。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 基类不包含本主题中讨论的方法的任何实现代码。 因此没有必要（但是无害）将对基类实现的调用添加到您自己的方法实现中。  
  
 有关如何在特定类型的脚本组件中使用的方法和属性，这些类的信息，请参阅明[Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。 该示例主题还包含完整的代码示例。  
  
## <a name="acquireconnections-method"></a>AcquireConnections 方法  
 源和目标通常必须连接到外部数据源。 请重写 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> 基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法，以从相应的连接管理器获得连接或连接信息。  
  
 下面的示例返回**System.Data.SqlClient.SqlConnection**从 ADO.NET 连接管理器。  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 下面的示例从平面文件连接管理器，返回的完整路径和文件名，然后打开通过的文件**System.IO.StreamReader**。  
  
```vb  
Private textReader As StreamReader  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    Dim connMgr As IDTSConnectionManager100 = _  
        Me.Connections.MyFlatFileSrcConnectionManager  
    Dim exportedAddressFile As String = _  
        CType(connMgr.AcquireConnection(Nothing), String)  
    textReader = New StreamReader(exportedAddressFile)  
  
End Sub  
```  
  
## <a name="preexecute-method"></a>PreExecute 方法  
 如果您有必须仅在开始处理数据行之前执行一次的处理，请重写 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PreExecute%2A> 基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 例如，在目标中，您可能希望配置参数化的命令，供目标将每个数据行插入到数据源中。  
  
```vb  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
...  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
```  
  
```csharp  
SqlConnection sqlConn;   
SqlCommand sqlCmd;   
SqlParameter sqlParam;   
  
public override void PreExecute()   
{   
  
    sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " + "VALUES(@addressid, @city)", sqlConn);   
    sqlParam = new SqlParameter("@addressid", SqlDbType.Int);   
    sqlCmd.Parameters.Add(sqlParam);   
    sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);   
    sqlCmd.Parameters.Add(sqlParam);   
  
}  
```  
  
## <a name="processing-inputs-and-outputs"></a>处理输入和输出  
  
### <a name="processing-inputs"></a>处理输入  
 配置为转换或目标的脚本组件有一个输入。  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>BufferWrapper 项目项提供的内容  
 为每个输入，你已配置， **BufferWrapper**项目项包含派生自的类<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>，并且具有相同名称作为输入。 每个输入缓冲区类包含以下属性、函数和方法：  
  
-   每个所选输入列的已命名类型化取值函数属性。 这些属性是只读的或读/写，具体取决于**使用类型**的列上指定**输入列**页**脚本转换编辑器**。  
  
-   A **\<列 > _IsNull**针对每个选择的属性输入列。 此属性也为只读或读/写，具体取决于**使用类型**指定的列。  
  
-   A **DirectRowTo\<outputbuffer >**配置每个方法的输出。 当筛选到一个在相同的多个输出行，将使用这些方法**ExclusionGroup**。  
  
-   A **NextRow**函数可获取下一步的输入的行，和**EndOfRowset**函数来确定是否已处理的最后一个缓冲区的数据。 你通常不需要这些函数使用输入处理方法中实现时**UserComponent**基类。 下一节提供有关的详细信息**UserComponent**基类。  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 项目项提供的内容  
 ComponentWrapper 项目项包含一个名为类**UserComponent**派生自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>。 **ScriptMain**在其中编写自定义代码的类派生自的反过来**UserComponent**。 **UserComponent**类包含以下方法：  
  
-   重写的实现**ProcessInput**方法。 这是数据流引擎调用下一步在运行时后的方法**PreExecute**方法，并可能多次调用。 **ProcessInput**移交到处理 **\<inputbuffer > _ProcessInput**方法。 则**ProcessInput**方法检查输入缓冲区的末尾，并且如果已到达缓冲区的末尾，调用可重写**FinishOutputs**方法和私有**MarkOutputsAsFinished**方法。 **MarkOutputsAsFinished**方法然后调用**SetEndOfRowset**对最后一个输出缓冲区。  
  
-   可重写实现 **\<inputbuffer > _ProcessInput**方法。 此默认实现只需循环访问每个输入的行和调用 **\<inputbuffer > _ProcessInputRow**。  
  
-   可重写实现 **\<inputbuffer > _ProcessInputRow**方法。 默认实现为空。 通常会重写此方法以编写自定义数据处理代码。  
  
#### <a name="what-your-custom-code-should-do"></a>自定义代码应执行的操作  
 你可以使用以下方法来处理中的输入**ScriptMain**类：  
  
-   重写 **\<inputbuffer > _ProcessInputRow**以处理每个输入行中的数据，通过传递。  
  
-   重写 **\<inputbuffer > _ProcessInput**仅当你需要执行一些其他操作时循环遍历输入行。 (例如，你需要测试**EndOfRowset**采取某种其他操作在所有已处理行。)调用 **\<inputbuffer > _ProcessInputRow**来执行行处理。  
  
-   重写**FinishOutputs**如果你需要做些什么到输出之前被关闭。  
  
 **ProcessInput**方法可确保在适当的时候调用这些方法。  
  
### <a name="processing-outputs"></a>处理输出  
 配置为源或转换的脚本组件有一个或多个输出。  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>BufferWrapper 项目项提供的内容  
 对于已配置的每个输出，BufferWrapper 项目项包含从 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 派生并且与输出同名的类。 每个输入缓冲区类包含以下属性和方法：  
  
-   每个输出列的已命名类型化只写取值函数属性。  
  
-   只写**\<列 > _IsNull**属性可用于将列的值设置为每个所选的输出列**null**。  
  
-   **AddRow**方法将空的新行添加到输出缓冲区。  
  
-   A **SetEndOfRowset**方法，以便知道的需更多的缓冲区数据的数据流引擎。 此外，还有**EndOfRowset**函数来确定当前缓冲区是否为最后一个缓冲区的数据。 你通常不需要这些函数使用输入处理方法中实现时**UserComponent**基类。  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 项目项提供的内容  
 ComponentWrapper 项目项包含一个名为类**UserComponent**派生自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>。 **ScriptMain**在其中编写自定义代码的类派生自的反过来**UserComponent**。 **UserComponent**类包含以下方法：  
  
-   重写的实现**PrimeOutput**方法。 数据流引擎调用此方法，然后才能**ProcessInput**在运行时，并仅调用一次。 **PrimeOutput**移交到处理**CreateNewOutputRows**方法。 然后，如果组件是源组件 （即，该组件具有没有输入）， **PrimeOutput**调用可重写**FinishOutputs**方法和私有**MarkOutputsAsFinished**方法。 **MarkOutputsAsFinished**方法调用**SetEndOfRowset**对最后一个输出缓冲区。  
  
-   可重写实现**CreateNewOutputRows**方法。 默认实现为空。 通常会重写此方法以编写自定义数据处理代码。  
  
#### <a name="what-your-custom-code-should-do"></a>自定义代码应执行的操作  
 你可以使用以下方法来处理中的输出**ScriptMain**类：  
  
-   重写**CreateNewOutputRows**仅当你可以添加并填充在处理输入的行之前输出行。 例如，你可以使用**CreateNewOutputRows**源中的数据，但具有异步输出的转换时，应调用**AddRow**期间或之后的输入数据的处理。  
  
-   重写**FinishOutputs**如果你需要做些什么到输出之前被关闭。  
  
 **PrimeOutput**方法可确保在适当的时候调用这些方法。  
  
## <a name="postexecute-method"></a>PostExecute 方法  
 如果您有必须仅在处理完数据行之后执行一次的处理，请重写 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> 基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 例如，在源中，你可能想要关闭**System.Data.SqlClient.SqlDataReader**你具有用于将数据加载到数据流。  
  
> [!IMPORTANT]  
>  集合**ReadWriteVariables**仅适用于**PostExecute**方法。 因此不能在处理每行数据时直接递增包变量的值， 相反，递增的值的局部变量，并将包变量的值设置为中的本地变量的值**PostExecute**方法之后的所有数据已处理。  
  
## <a name="releaseconnections-method"></a>ReleaseConnections 方法  
 源和目标通常必须连接到外部数据源。 请重写 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A> 基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法，以关闭和释放先前在 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> 方法中打开的连接。  
  
```vb  
    Dim connMgr As IDTSConnectionManager100  
...  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
```  
  
```csharp  
IDTSConnectionManager100 connMgr;  
  
public override void ReleaseConnections()  
{  
  
    connMgr.ReleaseConnection(sqlConn);  
  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [配置脚本组件编辑器中的脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [编码和调试脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

