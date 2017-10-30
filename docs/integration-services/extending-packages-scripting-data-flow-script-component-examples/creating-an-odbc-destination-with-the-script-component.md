---
title: "使用脚本组件创建 ODBC 目标 |Microsoft 文档"
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
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5eb539f0d18f473b10ed8d49bcee9c298292fb41
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>使用脚本组件创建 ODBC 目标
  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，你通常将数据保存到 ODBC 目标使用[!INCLUDE[vstecado](../../includes/vstecado-md.md)]目标和[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]ODBC 数据提供程序。 当然，还可以创建供单个包使用的即席 ODBC 目标。 若要创建此即席 ODBC 目标，可使用脚本组件，如下面的示例中所示。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个数据流任务和多个包的组件，请考虑以此脚本组件示例中的代码为基础，创建自定义数据流组件。 有关详细信息，请参阅 [开发自定义数据流组件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何创建目标组件，它使用一个现有的 ODBC 连接管理器以将数据从数据流入保存[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 此示例是自定义的修改的版本[!INCLUDE[vstecado](../../includes/vstecado-md.md)]目标，在主题中，已证实[使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 但是，在此示例中，自定义 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目标已修改为使用 ODBC 连接管理器并将数据保存到 ODBC 目标。 此外，还包括以下更改：  
  
-   不能调用**AcquireConnection**方法的 ODBC 连接管理器从托管代码，因为它返回本机对象。 因此，本示例使用连接管理器的连接字符串通过托管 ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 数据访问接口直接连接到数据源。  
  
-   **OdbcCommand**期望位置参数。 在命令的文本中，参数的位置由问号 (?) 指示。 (相比之下， **SqlCommand**需要命名的参数。)  
  
 此示例使用**Person.Address**表中**AdventureWorks**示例数据库。 该示例将第一个和第四个列中，  **int*AddressID** * 和**nvarchar (30) 城市**该数据工作流中此表的列。 在源、 转换和目标示例在主题中，使用此相同的数据[开发特定 Types of Script Components](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>配置此脚本组件示例  
  
1.  创建 ODBC 连接管理器连接到**AdventureWorks**数据库。  
  
2.  通过在运行以下 TRANSACT-SQL 命令创建的目标表**AdventureWorks**数据库：  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  向数据流设计器图面添加新的脚本组件并将其配置为目标。  
  
4.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中将上游源或转换的输出连接到目标组件。 （可以将源直接连接到目标，而不经任何转换。）若要确保此示例适用，上游组件的输出必须包含至少**AddressID**和**城市**中的列**Person.Address**表**AdventureWorks**示例数据库。  
  
5.  打开**脚本转换编辑器**。 上**输入列**页上，选择**AddressID**和**城市**列。  
  
6.  上**输入和输出**页上，如重命名更具描述性的名称与输入**MyAddressInput**。  
  
7.  上**连接管理器**页上，添加或创建 ODBC 连接管理器具有描述性名称如**MyODBCConnectionManager**。  
  
8.  上**脚本**页上，单击**编辑脚本**，然后输入下面中所示的脚本**ScriptMain**类。  
  
9. 关闭脚本开发环境中，关闭**脚本转换编辑器**，然后运行该示例。  
  
    ```vb  
    Imports System.Data.Odbc  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim odbcConn As OdbcConnection  
        Dim odbcCmd As OdbcCommand  
        Dim odbcParam As OdbcParameter  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connectionString As String  
            connectionString = Me.Connections.MyODBCConnectionManager.ConnectionString  
            odbcConn = New OdbcConnection(connectionString)  
            odbcConn.Open()  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            odbcCmd = New OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
                "VALUES(?, ?)", odbcConn)  
            odbcParam = New OdbcParameter("@addressid", OdbcType.Int)  
            odbcCmd.Parameters.Add(odbcParam)  
            odbcParam = New OdbcParameter("@city", OdbcType.NVarChar, 30)  
            odbcCmd.Parameters.Add(odbcParam)  
  
        End Sub  
  
        Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
            With odbcCmd  
                .Parameters("@addressid").Value = Row.AddressID  
                .Parameters("@city").Value = Row.City  
                .ExecuteNonQuery()  
            End With  
  
        End Sub  
  
        Public Overrides Sub ReleaseConnections()  
  
            odbcConn.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.Data.Odbc;  
    ...  
    public class ScriptMain :  
        UserComponent  
    {  
        OdbcConnection odbcConn;  
        OdbcCommand odbcCmd;  
        OdbcParameter odbcParam;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            string connectionString;  
            connectionString = this.Connections.MyODBCConnectionManager.ConnectionString;  
            odbcConn = new OdbcConnection(connectionString);  
            odbcConn.Open();  
  
        }  
  
        public override void PreExecute()  
        {  
  
            odbcCmd = new OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " +  
                "VALUES(?, ?)", odbcConn);  
            odbcParam = new OdbcParameter("@addressid", OdbcType.Int);  
            odbcCmd.Parameters.Add(odbcParam);  
            odbcParam = new OdbcParameter("@city", OdbcType.NVarChar, 30);  
            odbcCmd.Parameters.Add(odbcParam);  
  
        }  
  
        public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
        {  
  
            {  
                odbcCmd.Parameters["@addressid"].Value = Row.AddressID;  
                odbcCmd.Parameters["@city"].Value = Row.City;  
                odbcCmd.ExecuteNonQuery();  
            }  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            odbcConn.Close();  
  
        }  
    }  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  

