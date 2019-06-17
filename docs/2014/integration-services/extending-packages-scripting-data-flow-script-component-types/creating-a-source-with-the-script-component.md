---
title: 使用脚本组件创建源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d4a038fcc9db891b2c0a0155ffa2aba39d2f3759
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768663"
---
# <a name="creating-a-source-with-the-script-component"></a>使用脚本组件创建源
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的数据流中的源组件用于从数据源加载数据以传递到下游转换和目标。 通常通过现有连接管理器连接数据源。  
  
 有关脚本组件的概述，请参阅 [扩展使用脚本组件数据流] (../ extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md。  
  
 脚本组件及其生成的基础结构代码可以大大简化自定义数据流组件的开发过程。 但要了解脚本组件的工作原理，熟悉自定义数据流组件的开发步骤很有帮助。 请参阅[开发自定义数据流组件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)部分，特别是主题[开发自定义源组件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)。  
  
## <a name="getting-started-with-a-source-component"></a>开始一个源组件  
 向 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器的“数据流”窗格添加脚本组件时，“选择脚本组件类型”对话框将打开并提示你选择“源”、“目标”或“转换”脚本  。 在此对话框中选择“源”  。  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>在元数据设计模式下配置源组件  
 选择创建源组件后，可使用“脚本转换编辑器”配置该组件  。 有关详细信息，请参阅[在脚本组件编辑器中配置脚本组件](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 数据流源组件没有输入，支持一个或多个输出。 在编写自定义脚本之前，必须在元数据设计模式下完成的一个步骤是使用“脚本转换编辑器”配置组件的输出  。  
  
 还可以在“脚本转换编辑器”的“脚本”页上设置 ScriptLanguage 属性来指定脚本语言    。  
  
> [!NOTE]  
>  若要设置脚本组件和脚本任务的默认脚本语言，请使用“选项”对话框的“常规”页上的“脚本语言”选项    。 有关详细信息，请参阅 [General Page](../general-page-of-integration-services-designers-options.md)。  
  
### <a name="adding-connection-managers"></a>添加连接管理器  
 源组件通常使用现有连接管理器连接将其中的数据加载到数据流的数据源。 在“脚本转换编辑器”  的“连接管理器”  页中，单击“添加”  以添加适当的连接管理器。  
  
 但是，连接管理器只是一个封装和存储连接特定类型数据源必需信息的便利单元。 您必须编写自己的自定义代码才能加载或保存数据，并且才有可能打开和关闭与数据源的连接。  
  
 有关如何在脚本组件中使用连接管理器的常规信息，请参阅[在脚本组件中连接数据源](../extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
 有关“脚本转换编辑器”  的“连接管理器”  页的详细信息，请参阅[脚本转换编辑器（“连接管理器”页）](../script-transformation-editor-connection-managers-page.md)。  
  
### <a name="configuring-outputs-and-output-columns"></a>配置输出和输出列  
 源组件没有输入，支持一个或多个输出。 在“脚本转换编辑器”的“输入和输出”页中，已默认创建一个输出，但是还没有创建任何输出列   。 在编辑器的这一页，可能需要或希望配置以下各项。  
  
-   必须为每个输出手动添加和配置输出列。 为每个输出选择“输出列”文件夹，然后使用“添加列”和“删除列”按钮管理源组件的每个输出的输出列   。 随后，将使用在自动生成的代码中创建的类型化取值函数属性，在脚本中通过您在此处指定的名称来引用输出列。  
  
-   您可能希望创建一个或多个附加输出，如包含意外值的行的模拟错误输出。 使用“添加输出”和“删除输出”按钮可以管理源组件的输出   。 所有输入行都定向到所有可用输出，除非您还为以下一些输出的 `ExclusionGroup` 属性指定了相同的非零值，您要在这些输出中将每一行只定向到共享同一 `ExclusionGroup` 值的输出之一。 用于标识 `ExclusionGroup` 的所选特定整数值没有特殊要求。  
  
    > [!NOTE]  
    >  当您不希望输出所有行时，还可以对单个输出使用非零 `ExclusionGroup` 属性值。 但是，在这种情况下，必须为希望发送给输出的每一行显式调用 DirectRowTo\<outputbuffer> 方法  。  
  
-   您可以为输出指定一个友好名称。 随后，将使用在自动生成的代码中创建的类型化取值函数属性，在脚本中通过输出的名称来引用输出。  
  
-   通常，同一 `ExclusionGroup` 中的多个输出具有相同的输出列。 但是，如果要创建模拟的错误输出，则可能要添加多个列来存储错误信息。 有关数据流引擎如何处理错误行的信息，请参阅[在数据流组件中使用错误输出](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)。 但是，在脚本组件中，必须编写您自己的代码以便使用适当的错误信息填充这些附加列。 有关详细信息，请参阅[模拟脚本组件的错误输出](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 有关“脚本转换编辑器”  的“输入和输出”  页上的详细信息，请参阅[脚本转换编辑器（“输入和输出”页）](../script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>添加变量  
 如果有要在脚本中使用其值的任何现有变量，则可以添加在`ReadOnlyVariables`并`ReadWriteVariables`属性字段上**脚本**页**脚本转换编辑器**.  
  
 在属性字段中输入多个变量时，请用逗号将变量名隔开。 此外可以输入多个变量，通过单击省略号 ( **...** ) 按钮旁边`ReadOnlyVariables`并`ReadWriteVariables`属性字段和中的选择变量**选择变量**对话框。  
  
 有关如何在脚本组件中使用变量的常规信息，请参阅[在脚本组件中使用变量](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 有关“脚本转换编辑器”的“脚本”页的详细信息，请参阅[脚本转换编辑器（“脚本”页）](../script-transformation-editor-script-page.md)   。  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>在代码设计模式下编写源组件脚本  
 为组件配置完元数据后，可以打开 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 编写自定义脚本的代码。 若要打开 VSTA，请在“脚本转换编辑器”的“脚本”页中，单击“编辑脚本”    。 可使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 编写你的脚本，具体取决于为 ScriptLanguage 属性选择的脚本语言  。  
  
 有关适用于使用脚本组件创建的所有组件类型的重要信息，请参阅[脚本组件的编码和调试](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自动生成的代码  
 创建并配置源组件后打开 VSTA IDE 时，可编辑的 `ScriptMain` 类将显示在代码编辑器中。 您将在 `ScriptMain` 类中编写您的自定义代码。  
  
 `ScriptMain` 类包含 `CreateNewOutputRows` 方法的存根。 `CreateNewOutputRows` 是源组件中最重要的方法。  
  
 如果您打开**项目资源管理器**在 VSTA 中的窗口，可以看到，脚本组件还生成了只读`BufferWrapper`和`ComponentWrapper`项目项。 `ScriptMain` 类从 `UserComponent` 项目项中的 `ComponentWrapper` 类继承。  
  
 在运行时，数据流引擎调用 `PrimeOutput` 类中的 `UserComponent` 方法，该方法重写 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost.PrimeOutput%2A> 父类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 `PrimeOutput` 方法又调用下列方法：  
  
1.  `CreateNewOutputRows` 方法，在 `ScriptMain` 中要重写该方法，以将数据源中的行添加到最初为空的输出缓冲区中。  
  
2.  `FinishOutputs` 方法，默认情况下，该方法为空。 在 `ScriptMain` 中要重写此方法，以执行完成输出所需的任何处理。  
  
3.  私有的 `MarkOutputsAsFinished` 方法，该方法调用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> 父类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 方法来向数据流引擎指示输出已完成。 您无需在自己的代码中显式调用 `SetEndOfRowset`。  
  
### <a name="writing-your-custom-code"></a>编写自定义代码  
 为了完成创建自定义源组件，您可以在 `ScriptMain` 类的以下方法中编写脚本。  
  
1.  重写 `AcquireConnections` 方法以连接外部数据源。 从连接管理器中提取连接对象或者需要的连接信息。  
  
2.  如果可同时加载所有源数据，请重写 `PreExecute` 方法以加载数据。 例如，可以对连接到 `SqlCommand` 数据库的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后同时将所有源数据加载到 `SqlDataReader` 中。 如果必须每次加载一行源数据（例如，读取文本文件时），则可在 `CreateNewOutputRows` 中遍历行时加载数据。  
  
3.  使用重写的 `CreateNewOutputRows` 方法将新行添加到空的输出缓冲区中，然后在新输出行的每列中填充值。 使用每个输出缓冲区的 `AddRow` 方法来添加空的新行，然后设置每列的值。 通常，从外部源所加载的列复制值。  
  
4.  重写 `PostExecute` 方法以完成数据处理。 例如，可以关闭用于加载数据的 `SqlDataReader`。  
  
5.  如果需要，重写 `ReleaseConnections` 方法以断开与外部数据源的连接。  
  
## <a name="examples"></a>示例  
 下面的示例演示在 `ScriptMain` 类中创建源组件所需的自定义代码。  
  
> [!NOTE]  
>  这些示例使用**Person.Address**表中`AdventureWorks`示例数据库和传递它的第一个和第四个列**即 intaddressid 和**和**nvarchar (30) 市/县**列，在数据通过数据流。 在本节中，在源、转换和目标示例中使用相同的数据。 每个示例的其他前提条件和假设都记录在文档中。  
  
### <a name="adonet-source-example"></a>ADO.NET 源示例  
 本示例演示了使用现有 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中的数据加载到数据流中的源组件。  
  
 如果要运行此示例代码，必须按照如下方式配置包和组件：  
  
1.  创建使用 `SqlClient` 访问接口连接 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 数据库的 `AdventureWorks` 连接管理器。  
  
2.  向数据流设计器图面添加新的脚本组件并将其配置为源。  
  
3.  打开“脚本转换编辑器”  。 在“输入和输出”页中，用更具说明性的名称（如 MyAddressOutput）重命名默认输出，然后添加并配置两个输出列 AddressID 和 City     。  
  
    > [!NOTE]  
    >  确保将 City 输出列的数据类型更改为 DT_WSTR  。  
  
4.  在“连接管理器”页中，添加或创建 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器，并以诸如 MyADONETConnection 的名称命名   。  
  
5.  在“脚本”页中，单击“编辑脚本”并输入下面的脚本   。 然后关闭脚本开发环境和“脚本转换编辑器”  。  
  
6.  创建并配置目标组件，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标，或者[使用脚本组件创建目标](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中演示的示例目标组件，该组件需要 AddressID 和 City 列   。 然后将源组件连接到目标。 （无需任何转换，即可将源直接连接到目标。）在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据库中运行以下 `AdventureWorks` 命令，以创建目标表：  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  运行该示例。  
  
    ```vb  
    Imports System.Data.SqlClient  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim connMgr As IDTSConnectionManager100  
        Dim sqlConn As SqlConnection  
        Dim sqlReader As SqlDataReader  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            connMgr = Me.Connections.MyADONETConnection  
            sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim cmd As New SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn)  
            sqlReader = cmd.ExecuteReader  
  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Do While sqlReader.Read  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = sqlReader.GetInt32(0)  
                    .City = sqlReader.GetString(1)  
                End With  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
  
            sqlReader.Close()  
  
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
        SqlDataReader sqlReader;  
  
        public override void AcquireConnections(object Transaction)  
        {  
            connMgr = this.Connections.MyADONETConnection;  
            sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
  
            SqlCommand cmd = new SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn);  
            sqlReader = cmd.ExecuteReader();  
  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            while (sqlReader.Read())  
            {  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = sqlReader.GetInt32(0);  
                    MyAddressOutputBuffer.City = sqlReader.GetString(1);  
                }  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            sqlReader.Close();  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            connMgr.ReleaseConnection(sqlConn);  
  
        }  
  
    }  
    ```  
  
### <a name="flat-file-source-example"></a>平面文件源示例  
 本示例演示了使用现有平面文件连接管理器将平面文件中的数据加载到数据流中的源组件。 通过将平面文件源数据从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中导出来创建该数据。  
  
 如果要运行此示例代码，必须按照如下方式配置包和组件：  
  
1.  使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导导出**Person.Address**表从`AdventureWorks`到以逗号分隔的平面文件的示例数据库。 此示例使用文件名 ExportedAddresses.txt。  
  
2.  创建连接导出的数据文件的平面文件连接管理器。  
  
3.  向数据流设计器图面添加新的脚本组件并将其配置为源。  
  
4.  打开“脚本转换编辑器”  。 在“输入和输出”页中，用更具说明性的名称（如 MyAddressOutput）重命名默认输出   。 添加并配置两个输出列 AddressID 和 City   。  
  
5.  在“连接管理器”页中，添加或创建平面文件连接管理器，并以说明性的名称命名，如 MyFlatFileSrcConnectionManager   。  
  
6.  在“脚本”页中，单击“编辑脚本”并输入下面的脚本   。 然后关闭脚本开发环境和“脚本转换编辑器”  。  
  
7.  创建并配置目标组件，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标，或者[使用脚本组件创建目标](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中演示的示例目标组件。 然后将源组件连接到目标。 （无需任何转换，即可将源直接连接到目标。）在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据库中运行以下 `AdventureWorks` 命令，以创建目标表：  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  运行该示例。  
  
    ```vb  
    Imports System.IO  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Private textReader As StreamReader  
        Private exportedAddressFile As String  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connMgr As IDTSConnectionManager100 = _  
                Me.Connections.MyFlatFileSrcConnectionManager  
            exportedAddressFile = _  
                CType(connMgr.AcquireConnection(Nothing), String)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
            MyBase.PreExecute()  
            textReader = New StreamReader(exportedAddressFile)  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Dim nextLine As String  
            Dim columns As String()  
  
            Dim delimiters As Char()  
            delimiters = ",".ToCharArray  
  
            nextLine = textReader.ReadLine  
            Do While nextLine IsNot Nothing  
                columns = nextLine.Split(delimiters)  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = columns(0)  
                    .City = columns(3)  
                End With  
                nextLine = textReader.ReadLine  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
            MyBase.PostExecute()  
            textReader.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.IO;  
    public class ScriptMain:  
        UserComponent  
  
    {  
        private StreamReader textReader;  
        private string exportedAddressFile;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileSrcConnectionManager;  
            exportedAddressFile = (string)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
            base.PreExecute();  
            textReader = new StreamReader(exportedAddressFile);  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            string nextLine;  
            string[] columns;  
  
            char[] delimiters;  
            delimiters = ",".ToCharArray();  
  
            nextLine = textReader.ReadLine();  
            while (nextLine != null)  
            {  
                columns = nextLine.Split(delimiters);  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = columns[0];  
                    MyAddressOutputBuffer.City = columns[3];  
                }  
                nextLine = textReader.ReadLine();  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            base.PostExecute();  
            textReader.Close();  
  
        }  
  
    }  
    ```  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [使用脚本组件创建目标](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [开发自定义源组件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  
