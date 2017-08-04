---
title: "Connecting to Data Sources in the Script Task |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 825ff059476614085a338dd9c568031885bed64b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-task"></a>在脚本任务中连接数据源
  连接管理器提供对已在包中配置的数据源的访问。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](../../../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
 脚本任务可以访问这些连接管理器通过<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>属性**Dts**对象。 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合中的每个连接管理器都存储有关如何连接到基础数据源的信息。  
  
 调用连接管理器的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 方法时，如果连接管理器尚未连接数据源，则进行连接，然后返回供您在脚本任务代码中使用的相应连接或连接信息。  
  
> [!NOTE]  
>  你必须知道连接返回连接管理器之前调用的类型**AcquireConnection**。 因为脚本任务具有**Option Strict**启用，你必须强制转换的连接，作为类型返回**对象**，到适当的连接类型后，才能使用。  
  
 在代码中使用连接之前，可以使用 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> 属性返回的 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 方法查找现有连接。  
  
> [!IMPORTANT]  
>  不能调用 AcquireConnection 方法的返回非托管的对象，如 OLE DB 连接管理器和 Excel 连接管理器中，在脚本任务的托管代码中的连接管理器。 但是，你可以读取这些连接管理器中的 ConnectionString 属性，并连接到数据源在代码中直接使用的连接字符串具有**OledbConnection**从**System.Data.OleDb**命名空间。  
>   
>  如果你必须调用连接的 AcquireConnection 方法返回非托管的对象的管理器，使用[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]连接管理器。 配置 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 连接管理器为使用 OLE DB 访问接口时，该连接管理器使用用于 OLE DB 的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 数据访问接口进行连接。 在这种情况下，AcquireConnection 方法返回**System.Data.OleDb.OleDbConnection**而不是非托管对象。 若要配置[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]与 Excel 数据源，选择一起使用的连接管理器[!INCLUDE[msCoName](../../../includes/msconame-md.md)]OLE DB Provider for Jet，指定 Excel 文件，然后输入`Excel 8.0`（Excel 97 及更高版本） 的值作为**扩展属性**上**所有**页**连接管理器**对话框。  
  
## <a name="connections-example"></a>连接示例  
 下面的示例演示如何从脚本任务内部访问连接管理器。 该示例假定你已创建并配置[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]名为的连接管理器**测试 ADO.NET 连接**和名为平面文件连接管理器**测试平面文件连接**。 请注意，[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]连接管理器返回**SqlConnection**立即可以使用它连接到数据源的对象。 而平面文件连接管理器则只返回包含路径和文件名的字符串。 你必须使用从方法**System.IO**命名空间，若要打开和使用平面文件。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS &#41;连接](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [创建连接管理器](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
