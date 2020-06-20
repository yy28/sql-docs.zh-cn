---
title: 了解脚本组件对象模型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 80d61a4b4742163d999aa2f5d70e70336e680e27
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967242"
---
# <a name="understanding-the-script-component-object-model"></a>了解脚本组件对象模型
  如 [编写和调试脚本组件] （.）中所述。/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md，脚本组件项目包含三个项目项：

1.  `ScriptMain` 项，该项包含您要用来编写代码的 `ScriptMain` 类。 `ScriptMain` 类从 `UserComponent` 类继承。

2.  `ComponentWrapper` 项，包含 `UserComponent` 类，该类是 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>（包含用于处理数据和与包交互的方法和属性）的实例。 `ComponentWrapper` 项还包含 `Connections` 和 `Variables` 集合类。

3.  `BufferWrapper` 项，该项包含的类从每个输入和输出的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 继承，该项还包含每一列的类型化属性。

 当您在 `ScriptMain` 项中编写代码时，将使用本主题中讨论的对象、方法和属性。 每个组件不会用到此处列出的所有方法；但用到的方法都会按照此处所示的顺序。

 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 基类不包含本主题中讨论的方法的任何实现代码。 因此没有必要（但是无害）将对基类实现的调用添加到您自己的方法实现中。

 有关如何在特定类型的脚本组件中使用这些类的方法和属性的信息，请参阅[其他脚本组件示例](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)一节。 该示例主题还包含完整的代码示例。

## <a name="acquireconnections-method"></a>AcquireConnections 方法
 源和目标通常必须连接到外部数据源。 请重写 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> 基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法，以从相应的连接管理器获得连接或连接信息。

 下面的示例从 ADO.NET 连接管理器返回 `System.Data.SqlClient.SqlConnection`。

```vb
Dim connMgr As IDTSConnectionManager100
Dim sqlConn As SqlConnection

Public Overrides Sub AcquireConnections(ByVal Transaction As Object)

    connMgr = Me.Connections.MyADONETConnection
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)

End Sub
```

 下面的示例从平面文件连接管理器返回完整的路径和文件名，然后使用 `System.IO.StreamReader` 打开该文件。

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
 对于已配置的每个输入，`BufferWrapper` 项目项包含从 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 派生并且与输入同名的类。 每个输入缓冲区类包含以下属性、函数和方法：

-   每个所选输入列的已命名类型化取值函数属性。 这些属性是只读或读/写的，取决于在“脚本转换编辑器”的“输入列”页中为该列指定的“使用类型”    。

-   每个所选输入列的** \<column> _IsNull**属性。 此属性也是只读或读/写的，取决于为该列指定的“使用类型”  。

-   每个已配置输出的**DirectRowTo \<outputbuffer> **方法。 在将行筛选到位于同一 `ExclusionGroup` 中的多个输出之一时，将使用这些方法。

-   一个 `NextRow` 函数，用于获取下一个输入行，以及一个 `EndOfRowset` 函数，用于确定最后一个数据缓冲区是否已经处理。 使用在 `UserComponent` 基类中实现的输入处理方法时，通常不需要这些函数。 下一节提供有关 `UserComponent` 基类的详细信息。

#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 项目项提供的内容
 ComponentWrapper 项目项包含从 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 派生的名为 `UserComponent` 的类。 您要用来编写自定义代码的 `ScriptMain` 类又派生自 `UserComponent`。 `UserComponent` 类包含以下方法：

-   `ProcessInput` 方法的重写实现。 这是数据流引擎在运行时继调用 `PreExecute` 方法后调用的下一个方法，该方法可被调用多次。 `ProcessInput`将处理移交给** \<inputbuffer> _ProcessInput**方法。 然后 `ProcessInput` 方法检查是否已到达输入缓冲区的末尾，如果已到达缓冲区末尾，则调用可重写的 `FinishOutputs` 方法和私有 `MarkOutputsAsFinished` 方法。 然后 `MarkOutputsAsFinished` 方法对最后一个输出缓冲区调用 `SetEndOfRowset`。

-   ** \<inputbuffer> _ProcessInput**方法的可重写实现。 此默认实现只循环遍历每个输入行并调用** \<inputbuffer> _ProcessInputRow**。

-   ** \<inputbuffer> _ProcessInputRow**方法的可重写实现。 默认实现为空。 通常会重写此方法以编写自定义数据处理代码。

#### <a name="what-your-custom-code-should-do"></a>自定义代码应执行的操作
 可以使用以下方法在 `ScriptMain` 类中处理输入：

-   重写** \<inputbuffer> _ProcessInputRow** ，以在每个输入行通过时处理数据。

-   仅当在遍历输入行时需要执行其他操作时，才重写** \<inputbuffer> _ProcessInput** 。 （例如，在 `EndOfRowset` 处理完所有行之后，必须测试以执行其他一些操作。）调用** \<inputbuffer> _ProcessInputRow**以执行行处理。

-   如果必须在关闭输出之前对输出进行一些操作，请重写 `FinishOutputs`。

 `ProcessInput` 方法确保以合适的次数调用这些方法。

### <a name="processing-outputs"></a>处理输出
 配置为源或转换的脚本组件有一个或多个输出。

#### <a name="what-the-bufferwrapper-project-item-provides"></a>BufferWrapper 项目项提供的内容
 对于已配置的每个输出，BufferWrapper 项目项包含从 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 派生并且与输出同名的类。 每个输入缓冲区类包含以下属性和方法：

-   每个输出列的已命名类型化只写取值函数属性。

-   每个所选输出列的只写** \<column> _IsNull**属性，可用于将列值设置为 `null` 。

-   一个 `AddRow` 方法，用于将空的新行添加到输出缓冲区。

-   一个 `SetEndOfRowset` 方法，用于通知数据流引擎没有数据缓冲区了。 还有一个 `EndOfRowset` 函数，用于确定当前缓冲区是否是最后一个数据缓冲区。 当使用基类中实现的输入处理方法时，通常不需要这些函数 `UserComponent` 。

#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 项目项提供的内容
 ComponentWrapper 项目项包含从 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 派生的名为 `UserComponent` 的类。 您要用来编写自定义代码的 `ScriptMain` 类又派生自 `UserComponent`。 `UserComponent` 类包含以下方法：

-   `PrimeOutput` 方法的重写实现。 在运行时，数据流引擎在调用 `ProcessInput` 之前调用此方法，而且只调用一次。 `PrimeOutput` 将处理传送到 `CreateNewOutputRows` 方法。 然后，如果该组件是源（也就是说组件没有输入），则 `PrimeOutput` 调用可重写的 `FinishOutputs` 方法和私有 `MarkOutputsAsFinished` 方法。 `MarkOutputsAsFinished` 方法对最后一个输出缓冲区调用 `SetEndOfRowset`。

-   `CreateNewOutputRows` 方法的可重写实现。 默认实现为空。 通常会重写此方法以编写自定义数据处理代码。

#### <a name="what-your-custom-code-should-do"></a>自定义代码应执行的操作
 可以使用以下方法在 `ScriptMain` 类中处理输出：

-   仅当您可以在处理输入行之前添加和填充输出行时，重写 `CreateNewOutputRows`。 例如，可以在源中使用 `CreateNewOutputRows`，但在带有异步输出的转换中，应在输入数据处理期间或之后调用 `AddRow`。

-   如果必须在关闭输出之前对输出进行一些操作，请重写 `FinishOutputs`。

 `PrimeOutput` 方法确保以合适的次数调用这些方法。

## <a name="postexecute-method"></a>PostExecute 方法
 如果您有必须仅在处理完数据行之后执行一次的处理，请重写 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> 基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 例如，在源中，您可能希望关闭曾用来将数据加载到数据流中的 `System.Data.SqlClient.SqlDataReader`。

> [!IMPORTANT]
>  `ReadWriteVariables` 集合仅在 `PostExecute` 方法中可用。 因此不能在处理每行数据时直接递增包变量的值， 相反，增加局部变量的值，并在 `PostExecute` 处理完所有数据后将包变量的值设置为方法中的局部变量的值。

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

![Integration Services 图标（小）](../../media/dts-16.gif "集成服务图标（小）")**保持与 Integration Services 最**新  <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。

## <a name="see-also"></a>另请参阅
 [在脚本组件编辑器中配置脚本组件](configuring-the-script-component-in-the-script-component-editor.md)[编写和调试脚本组件] （.）/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md


