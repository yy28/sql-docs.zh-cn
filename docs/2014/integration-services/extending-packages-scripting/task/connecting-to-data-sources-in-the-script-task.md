---
title: 在脚本任务中连接数据源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
helpviewer_keywords:
- connections [Integration Services], scripts
- Integration Services packages, connections
- connection managers [Integration Services], scripts
- scripts [Integration Services], connections
- SSIS packages, connections
- packages [Integration Services], connections
- Script task [Integration Services], connections
- Connections property
- SQL Server Integration Services packages, connections
- SSIS Script task, connections
ms.assetid: 9c008380-715b-455b-9da7-22572d67c388
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 42511f1f79510d163c3211b3e0d82cb1ee2635ca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026808"
---
# <a name="connecting-to-data-sources-in-the-script-task"></a>在脚本任务中连接数据源
  连接管理器提供对已在包中配置的数据源的访问。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](../../connection-manager/integration-services-ssis-connections.md)。  
  
 脚本任务可通过 **Dts** 对象的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 属性访问这些连接管理器。 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合中的每个连接管理器都存储有关如何连接到基础数据源的信息。  
  
 调用连接管理器的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 方法时，如果连接管理器尚未连接数据源，则进行连接，然后返回供您在脚本任务代码中使用的相应连接或连接信息。  
  
> [!NOTE]  
>  你必须知道连接返回连接管理器之前调用的类型`AcquireConnection`。 由于脚本任务启用了 `Option Strict`，因此在使用连接之前，必须先将连接（返回类型为 `Object`）转换为适当的连接类型。  
  
 在代码中使用连接之前，可以使用 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> 属性返回的 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 方法查找现有连接。  
  
> [!IMPORTANT]  
>  在脚本任务的托管代码中，不能调用返回非托管对象的连接管理器（如 OLE DB 连接管理器和 Excel 连接管理器）的 AcquireConnection 方法。 但是，你可以读取这些连接管理器中的 ConnectionString 属性，并连接到数据源在代码中直接使用的连接字符串具有`OledbConnection`从**System.Data.OleDb**命名空间。  
>   
>  如果必须调用返回非托管对象的连接管理器的 AcquireConnection 方法，可使用 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 连接管理器。 配置 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 连接管理器为使用 OLE DB 访问接口时，该连接管理器使用用于 OLE DB 的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 数据访问接口进行连接。 在这种情况下，AcquireConnection 方法返回`System.Data.OleDb.OleDbConnection`而不是非托管对象。 若要将 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 连接管理器配置为用于 Excel 数据源，请选择 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for Jet，指定 Excel 文件，然后在“连接管理器”对话框的“全部”页上输入 `Excel 8.0`（对于 Excel 97 及更高版本）作为“扩展属性”的值。  
  
## <a name="connections-example"></a>连接示例  
 下面的示例演示如何从脚本任务内部访问连接管理器。 该示例假设已创建和配置了名为 **Test ADO.NET Connection** 的 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 连接管理器，以及名为 **Test Flat File Connection** 的平面文件连接管理器。 请注意，[!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 连接管理器返回可立即用于连接数据源的 `SqlConnection` 对象， 而平面文件连接管理器则只返回包含路径和文件名的字符串。 您必须使用 `System.IO` 命名空间中的方法来打开和使用该平面文件。  
  
```vb  
Public Sub Main()  
  
    Dim myADONETConnection As SqlClient.SqlConnection  
    myADONETConnection = _  
        DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction), _  
        SqlClient.SqlConnection)  
    MsgBox(myADONETConnection.ConnectionString, _  
        MsgBoxStyle.Information, "ADO.NET Connection")  
  
    Dim myFlatFileConnection As String  
    myFlatFileConnection = _  
        DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _  
        String)  
    MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
  
public class ScriptMain  
{  
  
        public void Main()  
        {  
            SqlConnection myADONETConnection = new SqlConnection();  
            myADONETConnection = (SqlConnection)(Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)as SqlConnection);  
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");  
  
            string myFlatFileConnection;  
            myFlatFileConnection = (string)(Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);  
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
  
```  
  
![集成服务图标 （小）](../../media/dts-16.gif "Integration Services 图标 （小）")**保持最新集成服务** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的集成服务页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 连接](../../connection-manager/integration-services-ssis-connections.md)   
 [创建连接管理器](../../create-connection-managers.md)  
  
  