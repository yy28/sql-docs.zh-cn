---
title: "使用脚本组件创建源 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-types
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
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4944c3d5752da21fed90f16a38a33b4fad41515
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-source-with-the-script-component"></a>使用脚本组件创建源
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的数据流中的源组件用于从数据源加载数据以传递到下游转换和目标。 通常通过现有连接管理器连接数据源。  
  
 脚本组件的概述，请参阅[Extending the Data Flow with Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 脚本组件及其生成的基础结构代码可以大大简化自定义数据流组件的开发过程。 但要了解脚本组件的工作原理，熟悉自定义数据流组件的开发步骤很有帮助。 请参阅明[开发自定义数据流组件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)，尤其是主题[开发自定义源组件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)。  
  
## <a name="getting-started-with-a-source-component"></a>开始一个源组件  
 当将脚本组件添加到的数据流窗格[!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器中，**选择脚本组件类型**对话框将打开，提示你选择的源、 目标或转换脚本。 在此对话框中，选择**源**。  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>在元数据设计模式下配置源组件  
 选择后创建源组件，请配置该组件使用**脚本转换编辑器**。 有关详细信息，请参阅[配置脚本组件编辑器中的脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 数据流源组件没有输入，支持一个或多个输出。 为该组件是必须使用在元数据设计模式下，完成的步骤之一配置输出**脚本转换编辑器**，需要在编写自定义脚本前。  
  
 此外可以通过设置指定的脚本语言**ScriptLanguage**属性**脚本**页**脚本转换编辑器**。  
  
> [!NOTE]  
>  若要设置的脚本组件和脚本任务的默认脚本语言，使用**脚本语言**选项**常规**页**选项**对话框。 有关详细信息，请参阅 [General Page](~/integration-services/control-flow/script-task-editor-general-page.md)。  
  
### <a name="adding-connection-managers"></a>添加连接管理器  
 源组件通常使用现有连接管理器连接将其中的数据加载到数据流的数据源。 上**连接管理器**页**脚本转换编辑器**，单击**添加**添加适当的连接管理器。  
  
 但是，连接管理器只是一个封装和存储连接特定类型数据源必需信息的便利单元。 您必须编写自己的自定义代码才能加载或保存数据，并且才有可能打开和关闭与数据源的连接。  
  
 有关如何使用脚本组件使用连接管理器的常规信息，请参阅[连接到脚本组件中的数据源](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
 有关详细信息**连接管理器**页**脚本转换编辑器**，请参阅[脚本转换编辑器 &#40;连接管理器页 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-outputs-and-output-columns"></a>配置输出和输出列  
 源组件没有输入，支持一个或多个输出。 上**输入和输出**页**脚本转换编辑器**，默认情况下，创建一个输出，但已创建任何输出列。 在编辑器的这一页，可能需要或希望配置以下各项。  
  
-   必须为每个输出手动添加和配置输出列。 选择每个输出的输出列文件夹，然后使用**添加列**和**删除列**按钮来管理每个输出源组件的输出列。 随后，将使用在自动生成的代码中创建的类型化取值函数属性，在脚本中通过您在此处指定的名称来引用输出列。  
  
-   您可能希望创建一个或多个附加输出，如包含意外值的行的模拟错误输出。 使用**添加输出**和**删除输出**按钮来管理源组件的输出。 所有输入的行定向到所有可用的输出中，除非还指定的相同非零值**ExclusionGroup**你想要直接只能对其中一个共享相同的输出的每一行这些输出的属性**ExclusionGroup**值。 特定的整数值选择标识**ExclusionGroup**并不重要。  
  
    > [!NOTE]  
    >  你还可以使用非零**ExclusionGroup**与单个输出时不希望输出所有行的属性值。 在这种情况下，但是，你必须明确地调用**DirectRowTo\<outputbuffer >**为你想要将发送到输出的每一行的方法。  
  
-   您可以为输出指定一个友好名称。 随后，将使用在自动生成的代码中创建的类型化取值函数属性，在脚本中通过输出的名称来引用输出。  
  
-   多个在相同的输出通常**ExclusionGroup**具有同一输出列。 但是，如果要创建模拟的错误输出，则可能要添加多个列来存储错误信息。 有关如何数据流引擎的信息处理错误行，请参阅[数据流组件中使用错误输出](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)。 但是，在脚本组件中，必须编写您自己的代码以便使用适当的错误信息填充这些附加列。 有关详细信息，请参阅[脚本组件为模拟错误输出](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 有关详细信息**输入和输出**页**脚本转换编辑器**，请参阅[脚本转换编辑器 （; 输入和输出页) #41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>添加变量  
 如果有任何现有的变量在脚本中你要使用其值，则可以添加在**ReadOnlyVariables**和**ReadWriteVariables**属性字段上**脚本**页**脚本转换编辑器**。  
  
 在属性字段中输入多个变量时，请用逗号将变量名隔开。 你也可以通过单击省略号输入多个变量 (**...**) 按钮旁边**ReadOnlyVariables**和**ReadWriteVariables**属性字段和中的选择变量**选择变量**对话框.  
  
 有关如何使用脚本组件中使用变量的常规信息，请参阅[Using Variables in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 有关详细信息**脚本**页**脚本转换编辑器**，请参阅[脚本转换编辑器 &#40;脚本页 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>在代码设计模式下编写源组件脚本  
 已为你的组件配置元数据后，打开[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 以自定义脚本中的代码。 若要打开 VSTA，请单击**编辑脚本**上**脚本**页**脚本转换编辑器**。 你可以通过使用编写你的脚本[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual C# 中，具体取决于为所选的脚本语言**ScriptLanguage**属性。  
  
 适用于所有类型的使用脚本组件创建的组件的重要信息，请参阅[编码和调试脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自动生成的代码  
 当在创建并配置源组件，可编辑后打开 VSTA IDE **ScriptMain**类会出现在代码编辑器中。 在编写自定义代码**ScriptMain**类。  
  
 **ScriptMain**类包括存根出于**CreateNewOutputRows**方法。 **CreateNewOutputRows**是源组件中最重要的方法。  
  
 如果你打开**项目资源管理器**在 VSTA 中的窗口中，你可以看到，脚本组件也具有生成只读**BufferWrapper**和**ComponentWrapper**项目项。 **ScriptMain**类继承自**UserComponent**类**ComponentWrapper**项目项。  
  
 在运行时，数据流引擎调用**PrimeOutput**中的方法**UserComponent**类，该类会重写<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父类。 **PrimeOutput**方法反过来调用以下方法：  
  
1.  **CreateNewOutputRows**方法，您在重写**ScriptMain**若要将行从数据源添加到输出缓冲区，它们是可清空在第一个。  
  
2.  **FinishOutputs**方法，默认为空。 重写此方法在**ScriptMain**以执行完成输出所需的任何处理。  
  
3.  私有**MarkOutputsAsFinished**方法，后者将调用<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>父类到数据流引擎指示输出已完成。 无需调用**SetEndOfRowset**在你自己的代码中显式。  
  
### <a name="writing-your-custom-code"></a>编写自定义代码  
 若要完成创建自定义源组件，你可能想要在中提供的以下方法中编写脚本**ScriptMain**类。  
  
1.  重写**AcquireConnections**方法连接到外部数据源。 从连接管理器中提取连接对象或者需要的连接信息。  
  
2.  重写**PreExecute**方法来加载数据时，如果你可以在同一时间加载所有源数据。 例如，可以执行**SqlCommand**针对[!INCLUDE[vstecado](../../includes/vstecado-md.md)]连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库并将所有源数据都加载在同一时间到**SqlDataReader**。 如果你必须将源数据一行加载 （例如，在读取文本文件时） 一次，你可以将数据加载如循环访问中的行**CreateNewOutputRows**。  
  
3.  使用经过重写**CreateNewOutputRows**方法，以将新行添加到空输出缓冲区，并以填充新的输出行中的每个列的值。 使用**AddRow**的每个输出缓冲区，以添加空的新行，并将每个列的值的方法。 通常，从外部源所加载的列复制值。  
  
4.  重写**PostExecute**方法以完成处理的数据。 例如，你可以关闭**SqlDataReader**你用来加载数据。  
  
5.  重写**ReleaseConnections**方法，如果需要从外部数据源断开连接。  
  
## <a name="examples"></a>示例  
 下面的示例演示自定义代码中所需**ScriptMain**类创建源组件。  
  
> [!NOTE]  
>  这些示例使用**Person.Address**表中**AdventureWorks**示例数据库并将传递其第一个和第四个列， **intAddressID**和**nvarchar (30) 城市**列，该数据工作流中的。 在本节中，在源、转换和目标示例中使用相同的数据。 每个示例的其他前提条件和假设都记录在文档中。  
  
### <a name="adonet-source-example"></a>ADO.NET 源示例  
 此示例演示了使用现有的源组件[!INCLUDE[vstecado](../../includes/vstecado-md.md)]连接管理器将数据从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到数据流的表。  
  
 如果要运行此示例代码，必须按照如下方式配置包和组件：  
  
1.  创建[!INCLUDE[vstecado](../../includes/vstecado-md.md)]使用连接管理器**SqlClient**访问接口连接到**AdventureWorks**数据库。  
  
2.  向数据流设计器图面添加新的脚本组件并将其配置为源。  
  
3.  打开**脚本转换编辑器**。 上**输入和输出**页上，重命名默认的输出与更具描述性的名称如**MyAddressOutput**，并添加和配置两个输出列， **AddressID**和**城市**。  
  
    > [!NOTE]  
    >  请务必更改的数据类型**城市**为 DT_WSTR 的输出列。  
  
4.  上**连接管理器**页上，添加或创建[!INCLUDE[vstecado](../../includes/vstecado-md.md)]连接管理器并为其提供一个名称如**MyADONETConnection**。  
  
5.  上**脚本**页上，单击**编辑脚本**和输入遵循的脚本。 然后关闭脚本开发环境和**脚本转换编辑器**。  
  
6.  创建和配置的目标组件，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标或所示的示例目标组件[使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)的**AddressID**和**城市**列。 然后将源组件连接到目标。 （可以将源直接连接到目标，而不经任何转换。）你可以通过运行以下命令，创建的目标表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**数据库：  
  
    ```sql
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
  
1.  使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导导出**Person.Address**表从**AdventureWorks**的以逗号分隔的平面文件的示例数据库。 此示例使用文件名 ExportedAddresses.txt。  
  
2.  创建连接导出的数据文件的平面文件连接管理器。  
  
3.  向数据流设计器图面添加新的脚本组件并将其配置为源。  
  
4.  打开**脚本转换编辑器**。 上**输入和输出**页上，重命名默认的输出与更具描述性的名称如**MyAddressOutput**。 添加和配置两个输出列， **AddressID**和**城市**。  
  
5.  上**连接管理器**页上，添加或创建平面文件连接管理器，如使用一个说明性名称**MyFlatFileSrcConnectionManager**。  
  
6.  上**脚本**页上，单击**编辑脚本**和输入遵循的脚本。 然后关闭脚本开发环境和**脚本转换编辑器**。  
  
7.  创建和配置的目标组件，如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标或所示的示例目标组件[使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 然后将源组件连接到目标。 （可以将源直接连接到目标，而不经任何转换。）你可以通过运行以下命令，创建的目标表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**数据库：  
  
    ```sql
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
  
## <a name="see-also"></a>另请参阅  
 [使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [开发自定义源组件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  

