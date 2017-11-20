---
title: "在脚本任务中使用变量 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], variables
- scripts [Integration Services], variables
- Variables property
- Variable object
- SSIS Script task, variables
- variables [Integration Services], Script task
ms.assetid: 593b5961-4bfa-4ce1-9531-a251c34e89d3
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ccfd7ce8e8f53d12dac3b021d5f62bd03947413d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-task"></a>在脚本任务中使用变量
  通过变量，脚本任务可以与包中的其他对象交换数据。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../../integration-services/integration-services-ssis-variables.md)。  
  
 脚本任务使用<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>属性**Dts**对象读取和写入<xref:Microsoft.SqlServer.Dts.Runtime.Variable>包中的对象。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A>属性<xref:Microsoft.SqlServer.Dts.Runtime.Variable>类是类型的**对象**。 因为脚本任务具有**Option Strict**启用，你必须转换<xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A>为后，才能使用适当的类型的属性。  
  
 添加到现有变量<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A>和<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A>中列出**脚本任务编辑器**要提供给自定义脚本。 请注意，变量名称区分大小写。 在该脚本中，你访问通过这两种类型的变量<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>属性**Dts**对象。 使用**值**属性来读取和写入到单个变量。 脚本任务在脚本读取和修改变量的值时，透明地管理锁定。  
  
 在代码中使用某个变量之前，可以使用 <xref:Microsoft.SqlServer.Dts.Runtime.Variables.Contains%2A> 属性返回的 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 集合的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 方法来检查该变量是否存在。  
  
 你还可以使用<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>属性 (Dts.VariableDispenser) 以便使用脚本任务中的变量。 使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> 时，您必须在您自己的代码中处理锁定语义和变量值的数据类型转换。 如果要使用在设计时不可用，而是以编程方式在运行时创建的变量，可能需要使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> 属性，而不是 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 属性。  
  
## <a name="using-the-script-task-within-a-foreach-loop-container"></a>在 Foreach 循环容器中使用脚本任务  
 当脚本任务在 Foreach 循环容器内重复运行时，脚本通常需要使用枚举器中当前项的内容。 例如，使用 Foreach 文件枚举器时，脚本需要知道当前文件名；使用 Foreach ADO 枚举器时，脚本需要知道当前数据行中各列的内容。  
  
 Foreach 循环容器与脚本任务之间的这种通信可以通过变量实现。 上**变量映射**页**Foreach 循环编辑器**，将变量分配给单个枚举项返回的数据的每个项。 例如，Foreach 文件枚举器仅返回索引 0 处的一个文件名，因此只需要一个变量映射，而在每行中返回多个数据列的枚举器需要将不同的变量映射到要在脚本任务中使用的每一列。  
  
 枚举的项映射到变量后，然后必须添加到映射的变量**ReadOnlyVariables**属性**脚本**页**脚本任务编辑器**要提供给你的脚本。 有关处理文件夹中的图像文件的 Foreach 循环容器内的脚本任务的示例，请参阅[处理与脚本任务的映像](../../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)。  
  
## <a name="variables-example"></a>变量示例  
 下面的示例演示如何在脚本任务中访问并使用变量，以确定包工作流的路径。 该示例假定你已创建了名为的整数变量`CustomerCount`和`MaxRecordCount`和路由添加到**ReadOnlyVariables**中的集合**脚本任务编辑器**。 `CustomerCount` 变量包含要导入的客户记录的数目。 如果其值大于 `MaxRecordCount` 的值，则脚本任务将报告失败。 如果因超过 `MaxRecordCount` 阈值而导致失败，则工作流的错误路径可实现任何所需的清除操作。  
  
 若要成功编译该示例，需要添加对 Microsoft.SqlServer.ScriptTask 程序集的引用。  
  
```vb  
Public Sub Main()  
  
    Dim customerCount As Integer  
    Dim maxRecordCount As Integer  
  
    If Dts.Variables.Contains("CustomerCount") = True AndAlso _  
        Dts.Variables.Contains("MaxRecordCount") = True Then  
  
        customerCount = _  
            CType(Dts.Variables("CustomerCount").Value, Integer)  
        maxRecordCount = _  
            CType(Dts.Variables("MaxRecordCount").Value, Integer)  
  
    End If  
  
    If customerCount > maxRecordCount Then  
            Dts.TaskResult = ScriptResults.Failure  
    Else  
            Dts.TaskResult = ScriptResults.Success  
    End If  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
    {  
        int customerCount;  
        int maxRecordCount;  
  
        if (Dts.Variables.Contains("CustomerCount")==true&&Dts.Variables.Contains("MaxRecordCount")==true)  
  
        {  
            customerCount = (int) Dts.Variables["CustomerCount"].Value;  
            maxRecordCount = (int) Dts.Variables["MaxRecordCount"].Value;  
  
        }  
  
        if (customerCount>maxRecordCount)  
        {  
            Dts.TaskResult = (int)ScriptResults.Failure;  
        }  
        else  
        {  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS &#41;变量](../../../integration-services/integration-services-ssis-variables.md)   
 [在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

