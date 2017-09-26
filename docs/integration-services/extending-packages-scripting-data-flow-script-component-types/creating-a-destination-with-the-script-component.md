---
title: "使用脚本组件创建目标 |Microsoft 文档"
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
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7680aac73590f92eadd615b9d164967e61877664
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-destination-with-the-script-component"></a>使用脚本组件创建目标
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的数据流中的目标组件用于将从上游源和转换接收的数据保存到数据源。 目标组件通常通过现有连接管理器连接数据源。  
  
 脚本组件的概述，请参阅[Extending the Data Flow with Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 脚本组件及其生成的基础结构代码可以大大简化自定义数据流组件的开发过程。 但是，若要了解脚本组件的工作原理，你可能发现很有用通读开发中的自定义数据流组件的步骤[开发自定义数据流组件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)部分中，尤其是[开发自定义的目标组件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)。  
  
## <a name="getting-started-with-a-destination-component"></a>开始一个目标组件  
 当将脚本组件添加到数据流选项卡的[!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器中，**选择脚本组件类型**对话框将打开，提示你选择**源**，**目标**，或**转换**脚本。 在此对话框中，选择**目标**。  
  
 然后，将转换的输出连接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中的目标组件。 出于测试目的，可以将源直接连接到目标，而不经任何转换。  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>在元数据设计模式下配置目标组件  
 通过选择此选项来创建目标组件后，配置该组件**脚本转换编辑器**。 有关详细信息，请参阅[配置脚本组件编辑器中的脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要选择脚本目标将使用的脚本语言，请设置**ScriptLanguage**属性**脚本**页**脚本转换编辑器**对话框。  
  
> [!NOTE]  
>  若要设置的默认脚本语言的脚本组件，使用**脚本语言**选项**常规**页**选项**对话框。 有关详细信息，请参阅 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
 数据流目标组件有一个输入，没有输出。 为该组件是必须使用在元数据设计模式下，完成的步骤之一配置输入**脚本转换编辑器**，需要在编写自定义脚本前。  
  
### <a name="adding-connection-managers"></a>添加连接管理器  
 目标组件通常使用现有连接管理器连接将数据流中的数据保存到的数据源。 上**连接管理器**页**脚本转换编辑器**，单击**添加**添加适当的连接管理器。  
  
 但是，连接管理器只是一个封装和存储连接特定类型数据源所需信息的便利单元。 您必须编写自己的自定义代码才能加载或保存数据，并且才有可能打开和关闭与数据源的连接。  
  
 有关如何使用脚本组件使用连接管理器的常规信息，请参阅[连接到脚本组件中的数据源](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
 有关详细信息**连接管理器**页**脚本转换编辑器**，请参阅[脚本转换编辑器 &#40;连接管理器页 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>配置输入和输入列  
 目标组件有一个输入，没有输出。  
  
 上**输入列**页**脚本转换编辑器**，列列表显示可用列从上游组件的输出数据流中的数据。 选择要保存的列。  
  
 有关详细信息**输入列**页**脚本转换编辑器**，请参阅[脚本转换编辑器 （; 输入列页) #41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)。  
  
 **输入和输出**页**脚本转换编辑器**显示的单个输入，你可以重命名。 通过使用在自动生成的代码中创建的取值函数属性，在脚本中将通过输入的名称来引用输入。  
  
 有关详细信息**输入和输出**页**脚本转换编辑器**，请参阅[脚本转换编辑器 （; 输入和输出页) #41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>添加变量  
 如果你想要在脚本中使用现有的变量，则可以添加在**ReadOnlyVariables**和**ReadWriteVariables**属性字段上**脚本**页**脚本转换编辑器**。  
  
 在属性字段中添加多个变量时，请用逗号将变量名隔开。 此外可以选择多个变量，通过单击省略号 (**...**) 按钮旁边**ReadOnlyVariables**和**ReadWriteVariables**属性字段，然后选择中的变量**选择变量**对话框。  
  
 有关如何使用脚本组件中使用变量的常规信息，请参阅[Using Variables in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 有关详细信息**脚本**页**脚本转换编辑器**，请参阅[脚本转换编辑器 &#40;脚本页 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>在代码设计模式下编写目标组件脚本  
 为组件配置完元数据后，可以编写自定义脚本。 在**脚本转换编辑器**上**脚本**页上，单击**编辑脚本**以打开[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE你可在其中添加自定义脚本。 你使用的脚本语言取决于你是选择还是[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual C# 作为的脚本语言**ScriptLanguage**属性**脚本**页。  
  
 适用于所有类型的使用脚本组件创建的组件的重要信息，请参阅[编码和调试脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自动生成的代码  
 当你打开 VSTA IDE 后你创建和配置目标组件，可编辑**ScriptMain**类将出现在代码编辑器中使用存根出于**ProcessInputRow**方法。 **ScriptMain**类是你将在其中编写自定义代码，和**ProcessInputRow**是目标组件中最重要的方法。  
  
 如果你打开**项目资源管理器**在 VSTA 中的窗口中，你可以看到，脚本组件也具有生成只读**BufferWrapper**和**ComponentWrapper**项目项。 **ScriptMain**类继承自**UserComponent**类**ComponentWrapper**项目项。  
  
 在运行时，数据流引擎调用**ProcessInput**中的方法**UserComponent**类，该类会重写<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父类。 **ProcessInput**方法反过来循环访问的输入的缓冲区和调用中的行**ProcessInputRow**方法一次为每个行。  
  
### <a name="writing-your-custom-code"></a>编写自定义代码  
 若要完成创建自定义的目标组件，你可能想要在中提供的以下方法中编写脚本**ScriptMain**类。  
  
1.  重写**AcquireConnections**方法连接到外部数据源。 从连接管理器中提取连接对象或者需要的连接信息。  
  
2.  重写**PreExecute**方法若要准备将数据保存。 例如，你可能想要创建和配置**SqlCommand**和此方法中的使用其参数。  
  
3.  使用经过重写**ProcessInputRow**方法来将每个输入的行复制到外部数据源。 例如，对于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标，可以将列的值复制到的参数**SqlCommand**并执行一次为每个行的命令。 为平面文件目标，你可以编写到每个列的值**StreamWriter**，由列分隔符分隔各个值。  
  
4.  重写**PostExecute**方法，如果需要，从外部数据源断开连接并执行任何其他所需的清理。  
  
## <a name="examples"></a>示例  
 下面的示例演示代码中所需**ScriptMain**类，以便创建目标组件。  
  
> [!NOTE]  
>  这些示例使用**Person.Address**表中**AdventureWorks**示例数据库并将传递其第一个和第四个列， * *int*AddressID** * 和**nvarchar (30) 城市**列，该数据工作流中的。 在本节中，在源、转换和目标示例中使用相同的数据。 每个示例的其他前提条件和假设都记录在文档中。  
  
### <a name="adonet-destination-example"></a>ADO.NET 目标示例  
 此示例演示了使用现有的目标组件[!INCLUDE[vstecado](../../includes/vstecado-md.md)]连接管理器以将数据从数据流入保存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 如果要运行此示例代码，必须按照如下方式配置包和组件：  
  
1.  创建[!INCLUDE[vstecado](../../includes/vstecado-md.md)]使用连接管理器**SqlClient**访问接口连接到**AdventureWorks**数据库。  
  
2.  通过运行以下命令，创建的目标表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**数据库：  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  向数据流设计器图面添加新的脚本组件并将其配置为目标。  
  
4.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中将上游源或转换的输出连接到目标组件。 （可以将源直接连接到目标，而不经任何转换。）此输出应提供从数据**Person.Address**表**AdventureWorks**包含的示例数据库至少**AddressID**和**城市**列。  
  
5.  打开**脚本转换编辑器**。 上**输入列**页上，选择**AddressID**和**城市**输入列。  
  
6.  上**输入和输出**页上，如重命名更具描述性的名称与输入**MyAddressInput**。  
  
7.  上**连接管理器**页上，添加或创建[!INCLUDE[vstecado](../../includes/vstecado-md.md)]如同名的连接管理器**MyADONETConnectionManager**。  
  
8.  上**脚本**页上，单击**编辑脚本**和输入遵循的脚本。 然后关闭脚本开发环境。  
  
9. 关闭**脚本转换编辑器**和运行示例。  
  
```vb  
Imports System.Data.SqlClient  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim connMgr As IDTSConnectionManager100  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        connMgr = Me.Connections.MyADONETConnectionManager  
        sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
        With sqlCmd  
            .Parameters("@addressid").Value = Row.AddressID  
            .Parameters("@city").Value = Row.City  
            .ExecuteNonQuery()  
        End With  
    End Sub  
  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.Data.SqlClient;  
public class ScriptMain:  
    UserComponent  
  
{  
    IDTSConnectionManager100 connMgr;  
    SqlConnection sqlConn;  
    SqlCommand sqlCmd;  
    SqlParameter sqlParam;  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        connMgr = this.Connections.MyADONETConnectionManager;  
        sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " +  
            "VALUES(@addressid, @city)", sqlConn);  
        sqlParam = new SqlParameter("@addressid", SqlDbType.Int);  
        sqlCmd.Parameters.Add(sqlParam);  
        sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);  
        sqlCmd.Parameters.Add(sqlParam);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
        {  
            sqlCmd.Parameters["@addressid"].Value = Row.AddressID;  
            sqlCmd.Parameters["@city"].Value = Row.City;  
            sqlCmd.ExecuteNonQuery();  
        }  
    }  
  
    public override void ReleaseConnections()  
    {  
  
        connMgr.ReleaseConnection(sqlConn);  
  
    }  
  
}  
```  
  
### <a name="flat-file-destination-example"></a>平面文件目标示例  
 本示例演示了使用现有平面文件连接管理器将数据流中的数据保存到平面文件中的目标组件。  
  
 如果要运行此示例代码，必须按照如下方式配置包和组件：  
  
1.  创建连接目标文件的平面文件连接管理器。 该文件不必一定存在，目标组件会创建它。 配置为以逗号分隔的文件，以便包含目标文件**AddressID**和**城市**列。  
  
2.  向数据流设计器图面添加新的脚本组件并将其配置为目标。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中将上游源或转换的输出连接到目标组件。 （可以将源直接连接到目标，而不经任何转换。）此输出应提供从数据**Person.Address**表**AdventureWorks**示例数据库，并且应包含至少**AddressID**和**城市**列。  
  
4.  打开**脚本转换编辑器**。 上**输入列**页上，选择**AddressID**和**城市**列。  
  
5.  上**输入和输出**页上，将重命名替换为更具描述性的名称，输入如**MyAddressInput**。  
  
6.  上**连接管理器**页上，添加或创建平面文件连接管理器具有描述性名称如**MyFlatFileDestConnectionManager**。  
  
7.  上**脚本**页上，单击**编辑脚本**和输入遵循的脚本。 然后关闭脚本开发环境。  
  
8.  关闭**脚本转换编辑器**和运行示例。  
  
```vb  
Imports System.IO  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim copiedAddressFile As String  
    Private textWriter As StreamWriter  
    Private columnDelimiter As String = ","  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        Dim connMgr As IDTSConnectionManager100 = _  
            Me.Connections.MyFlatFileDestConnectionManager  
        copiedAddressFile = CType(connMgr.AcquireConnection(Nothing), String)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        textWriter = New StreamWriter(copiedAddressFile, False)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With textWriter  
            If Not Row.AddressID_IsNull Then  
                .Write(Row.AddressID)  
            End If  
            .Write(columnDelimiter)  
            If Not Row.City_IsNull Then  
                .Write(Row.City)  
            End If  
            .WriteLine()  
        End With  
  
    End Sub  
  
    Public Overrides Sub PostExecute()  
  
        textWriter.Close()  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.IO;  
public class ScriptMain:  
    UserComponent  
  
{  
    string copiedAddressFile;  
    private StreamWriter textWriter;  
    private string columnDelimiter = ",";  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileDestConnectionManager;  
        copiedAddressFile = (string) connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        textWriter = new StreamWriter(copiedAddressFile, false);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            if (!Row.AddressID_IsNull)  
            {  
                textWriter.Write(Row.AddressID);  
            }  
            textWriter.Write(columnDelimiter);  
            if (!Row.City_IsNull)  
            {  
                textWriter.Write(Row.City);  
            }  
            textWriter.WriteLine();  
        }  
  
    }  
  
    public override void PostExecute()  
    {  
  
        textWriter.Close();  
  
    }  
  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用脚本组件创建源](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [开发自定义的目标组件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
