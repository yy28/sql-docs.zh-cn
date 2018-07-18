---
title: 加载本地包的输出 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c7b0056def4b62d7305fe5ac78db93ba15fb22a8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254629"
---
# <a name="loading-the-output-of-a-local-package"></a>加载本地包的输出
  使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 将输出保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标，或使用 System.IO 命名空间中的类将输出保存到平面文件目标时，客户端应用程序即可读取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的输出。 但是，客户端应用程序也可以直接从内存读取包的输出，而无需中间步骤来持久化这些数据。 此解决方案的关键在于`Microsoft.SqlServer.Dts.DtsClient`命名空间，其中包含专门的实现`IDbConnection`， `IDbCommand`，和**IDbDataParameter**接口从**System.Data**命名空间。 默认情况下，程序集 Microsoft.SqlServer.Dts.DtsClient.dll 安装在 %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn 中。  
  
> [!NOTE]  
>  本主题介绍的过程要求数据流任务以及所有父对象的 DelayValidation 属性均设置为其默认值 False。  
  
## <a name="description"></a>Description  
 本过程说明如何使用托管代码开发客户端应用程序，该应用程序使用 DataReader 目标直接从内存加载包的输出。 此处总结的步骤在随后的代码示例中演示。  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>将数据包输出加载到客户端应用程序中  
  
1.  在包中，配置 DataReader 目标，以接收要读入到客户端应用程序中的输出。 使用说明性的名称为 DataReader 目标命名，因为您稍后将在客户端应用程序中使用此名称。 请记录 DataReader 目标的名称。  
  
2.  在开发项目中，将引用设置为`Microsoft.SqlServer.Dts.DtsClient`命名空间中查找程序集**Microsoft.SqlServer.Dts.DtsClient.dll**。 默认情况下，此程序集安装在 C:\Program Files\Microsoft SQL Server\100\DTS\Binn 中。 导入到你的代码使用 C# 命名空间`Using`或[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]`Imports`语句。  
  
3.  在代码中，创建类型的对象`DtsClient.DtsConnection`包含所需的命令行参数的连接字符串**dtexec.exe**运行包。 有关详细信息，请参阅 [dtexec Utility](../packages/dtexec-utility.md)。 然后，使用此连接字符串打开连接。 还可以使用 dtexecui 实用工具直观地创建所需的连接字符串。  
  
    > [!NOTE]  
    >  该示例代码演示如何使用 `/FILE <path and filename>` 语法从文件系统加载包。 但您也可以使用 `/SQL <package name>` 语法从 MSDB 数据库加载包，或者使用 `/DTS \<folder name>\<package name>` 语法从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包存储区加载包。  
  
4.  创建类型为 `DtsClient.DtsCommand` 的对象，该对象使用先前创建的 `DtsConnection`，并将该对象的 `CommandText` 属性设置为包中 DataReader 目标的名称。 然后，调用命令对象的 `ExecuteReader` 方法以将包结果加载到新的 DataReader 中。  
  
5.  还可以通过对 `DtsDataParameter` 对象使用 `DtsCommand` 对象的集合来间接参数化包的输出，以将值传递给在包中定义的变量。 在包中，您可以使用这些变量作为查询参数或在表达式中使用这些变量以影响返回给 DataReader 目标的结果。 必须在包中定义这些变量**DtsClient**命名空间才能使用它们与`DtsDataParameter`从客户端应用程序的对象。 （可能需要单击“变量”窗口中的“选择变量列”工具栏按钮才会显示“命名空间”列。）在您的客户端代码中，向 `DtsDataParameter` 的 `Parameters` 集合添加 `DtsCommand` 时，可省略变量名称的 DtsClient 命名空间引用。 例如：  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  根据需要重复调用 DataReader 的 `Read` 方法以遍历输出数据的各行。 使用这些数据，或将这些数据保存在客户端应用程序，以供将来使用。  
  
    > [!IMPORTANT]  
    >  读取最后一行数据后，此 DataReader 实现的 `Read` 方法将再返回一次 `true`。 因此在 `Read` 返回 `true` 时很难使用遍历 DataReader 的常规代码。 如果您的代码在读取预期行数后尝试关闭 DataReader 或连接，而不对 `Read` 方法进行附加的最终调用时，该代码将引发未处理的异常。 但是，如果您的代码尝试在此循环的最后一轮操作中读取数据，则在 `Read` 仍返回 `true` 而最后一行已传递时，该代码将引发未处理的 `ApplicationException`，并包含消息“SSIS IDataReader 已到达结果集末尾”。 此行为与其他 DataReader 实现的行为不同。 因此，使用循环读取 DataReader 中的各行，而 `Read` 返回 `true` 时，您需要针对上次成功调用 `ApplicationException` 方法编写代码以捕获、测试和放弃此预期的 `Read`。 或者，如果您事先知道应读取的行数，则可以处理这些行，然后在关闭 DataReader 和连接之前再调用一次 `Read` 方法。  
  
7.  调用 `Dispose` 对象的 `DtsCommand` 方法。 如果已使用任何 `DtsDataParameter` 对象，这样做尤其重要。  
  
8.  关闭 DataReader 和连接对象。  
  
## <a name="example"></a>示例  
 下面的示例将运行一个包，用于计算单个聚合值并将该值保存到 DataReader 目标，然后从 DataReader 读取此值，并在 Windows 窗体的文本框中显示该值。  
  
 在将包的输出加载到客户端应用程序时不一定要使用参数。 如果不希望使用的参数，可以省略中的变量的使用**DtsClient**命名空间，并省略使用的代码`DtsDataParameter`对象。  
  
#### <a name="to-create-the-test-package"></a>创建测试包  
  
1.  创建新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。 示例代码使用“DtsClientWParamPkg.dtsx”作为包的名称。  
  
2.  在 DtsClient 命名空间中添加类型为 String 的变量。 示例代码使用 Country 作为该变量的名称。 （可能需要单击“变量”窗口中的“选择变量列”工具栏按钮才会显示“命名空间”列。）  
  
3.  添加用于连接 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 示例数据库的 OLE DB 连接管理器。  
  
4.  向包添加数据流任务，并切换到数据流设计图面。  
  
5.  向数据流添加 OLE DB 源，并将其配置为使用之前创建的 OLE DB 连接管理器以及下面的 SQL 命令：  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  单击`Parameters`，然后在**设置查询参数**对话框框中，将一个输入的参数在查询中，Parameter0 映射到 dtsclient:: Country 变量。  
  
7.  向数据流添加聚合转换，并将 OLE DB 源的输出连接到该转换。 打开聚合转换编辑器，将其配置为对所有输入列 (*) 执行“COUNT ALL”运算，并以别名 CustomerCount 输出聚合值。  
  
8.  向数据流添加 DataReader 目标，并将聚合转换的输出连接到 DataReader 目标。 示例代码使用“DataReaderDest”作为 DataReader 的名称。 为目标选择单个可用输入列 CustomerCount。  
  
9. 保存包。 接下来要创建的测试应用程序将运行该包并直接从内存检索其输出。  
  
#### <a name="to-create-the-test-application"></a>创建测试应用程序  
  
1.  创建新的 Windows 窗体应用程序。  
  
2.  添加对的引用`Microsoft.SqlServer.Dts.DtsClient`通过浏览到中具有相同名称的程序集的命名空间 **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**。  
  
3.  复制以下示例代码并将其粘贴到窗体的代码模块中。  
  
4.  修改的值`dtexecArgs`变量根据需要使该变量包含所需的命令行参数**dtexec.exe**运行包。 示例代码从文件系统加载包。  
  
5.  值修改`dataReaderName`变量根据需要使该变量包含包中 DataReader 目标的名称。  
  
6.  在窗体中放入一个按钮和一个文本框。 示例代码使用`btnRun`作为按钮的名称和`txtResults`作为文本框的名称。  
  
7.  运行该应用程序并单击按钮。 在短暂运行包后，您应能够看到在窗体的文本框中显示由包计算的聚合值（Canada 的客户计数）。  
  
### <a name="sample-code"></a>示例代码  
  
```vb  
Imports System.Data  
Imports Microsoft.SqlServer.Dts.DtsClient  
  
Public Class Form1  
  
  Private Sub btnRun_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnRun.Click  
  
    Dim dtexecArgs As String  
    Dim dataReaderName As String  
    Dim countryName As String  
  
    Dim dtsConnection As DtsConnection  
    Dim dtsCommand As DtsCommand  
    Dim dtsDataReader As IDataReader  
    Dim dtsParameter As DtsDataParameter  
  
    Windows.Forms.Cursor.Current = Cursors.WaitCursor  
  
    dtexecArgs = "/FILE ""C:\...\DtsClientWParamPkg.dtsx"""  
    dataReaderName = "DataReaderDest"  
    countryName = "Canada"  
  
    dtsConnection = New DtsConnection()  
    With dtsConnection  
      .ConnectionString = dtexecArgs  
      .Open()  
    End With  
  
    dtsCommand = New DtsCommand(dtsConnection)  
    dtsCommand.CommandText = dataReaderName  
  
    dtsParameter = New DtsDataParameter("Country", DbType.String)  
    dtsParameter.Direction = ParameterDirection.Input  
    dtsCommand.Parameters.Add(dtsParameter)  
  
    dtsParameter.Value = countryName  
  
    dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default)  
  
    With dtsDataReader  
      .Read()  
      txtResults.Text = .GetInt32(0).ToString("N0")  
    End With  
  
    'After reaching the end of data rows,  
    ' call the Read method one more time.  
    Try  
      dtsDataReader.Read()  
    Catch ex As Exception  
      MessageBox.Show("Exception on final call to Read method:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception on final call to Read method", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    ' The following method is a best practice, and is  
    '  required when using DtsDataParameter objects.  
    dtsCommand.Dispose()  
  
    Try  
      dtsDataReader.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing DataReader:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing DataReader", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Try  
      dtsConnection.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing connection:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing connection", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Windows.Forms.Cursor.Current = Cursors.Default  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Data;  
using Microsoft.SqlServer.Dts.DtsClient;  
  
namespace DtsClientWParamCS  
{  
  public partial class Form1 : Form  
  {  
    public Form1()  
    {  
      InitializeComponent();  
      this.btnRun.Click += new System.EventHandler(this.btnRun_Click);  
    }  
  
    private void btnRun_Click(object sender, EventArgs e)  
    {  
      string dtexecArgs;  
      string dataReaderName;  
      string countryName;  
  
      DtsConnection dtsConnection;  
      DtsCommand dtsCommand;  
      IDataReader dtsDataReader;  
      DtsDataParameter dtsParameter;  
  
      Cursor.Current = Cursors.WaitCursor;  
  
      dtexecArgs = @"/FILE ""C:\...\DtsClientWParamPkg.dtsx""";  
      dataReaderName = "DataReaderDest";  
      countryName = "Canada";  
  
      dtsConnection = new DtsConnection();  
      {  
        dtsConnection.ConnectionString = dtexecArgs;  
        dtsConnection.Open();  
      }  
  
      dtsCommand = new DtsCommand(dtsConnection);  
      dtsCommand.CommandText = dataReaderName;  
  
      dtsParameter = new DtsDataParameter("Country", DbType.String);  
      dtsParameter.Direction = ParameterDirection.Input;  
      dtsCommand.Parameters.Add(dtsParameter);  
  
      dtsParameter.Value = countryName;  
  
      dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default);  
  
      {  
        dtsDataReader.Read();  
        txtResults.Text = dtsDataReader.GetInt32(0).ToString("N0");  
      }  
  
      //After reaching the end of data rows,  
      // call the Read method one more time.  
      try  
      {  
        dtsDataReader.Read();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception on final call to Read method:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception on final call to Read method", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      // The following method is a best practice, and is  
      //  required when using DtsDataParameter objects.  
      dtsCommand.Dispose();  
  
      try  
      {  
        dtsDataReader.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing DataReader:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing DataReader", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      try  
      {  
        dtsConnection.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing connection:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing connection", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      Cursor.Current = Cursors.Default;  
  
    }  
  }  
}  
```  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [了解本地和远程执行之间的区别](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [以编程方式加载和运行本地包](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [以编程方式加载和运行远程包](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  
