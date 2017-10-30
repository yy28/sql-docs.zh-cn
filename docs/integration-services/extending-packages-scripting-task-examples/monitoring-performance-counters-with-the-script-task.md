---
title: "监视性能计数器 with the Script Task |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- performance counters [Integration Services]
- SSIS Script task, performance counters
- custom performance counters [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], performance counters
- counters [Integration Services]
ms.assetid: 86609bf1-cae6-435e-a58d-41bdfc521e94
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: fd733f7d2fdf9c5d1181df6e7856d729e9a58026
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="monitoring-performance-counters-with-the-script-task"></a>使用脚本任务监视性能计数器
  管理员可能需要监视对大量数据执行复杂转换的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的性能。 **System.Diagnostics**命名空间的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]提供的类，使用现有的性能计数器和创建性能计数器。  
  
 性能计数器存储应用程序的性能信息，您可以利用这些信息分析软件在一段时间内的性能。 性能计数器可以使用来监视本地或远程**性能监视器**工具。 您可以将性能计数器的值存储在变量中，用于以后在包中进行控制流分支跳转。  
  
 作为使用性能计数器的替代方法，你可以将提升<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A>通过事件<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>属性**Dts**对象。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> 事件向 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 运行时返回增量进度和完成的百分比信息。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下面的示例创建一个自定义性能计数器并递增该计数器。 首先，该示例确定性能计数器是否已存在。 如果性能计数器尚未创建，脚本调用**创建**方法**PerformanceCounterCategory**对象来创建它。 创建性能计数器后，脚本将递增该计数器。 最后，该示例遵循最佳做法的调用**关闭**上不再需要时的性能计数器的方法。  
  
> [!NOTE]  
>  创建新的性能计数器类别和性能计数器需要管理权限。 此外，新类别和计数器在创建后将持久存在于计算机中。  
  
#### <a name="to-configure-this-script-task-example"></a>配置此脚本任务示例  
  
-   使用**导入**代码来导入语句**System.Diagnostics**命名空间。  
  
### <a name="example-code"></a>示例代码  
  
```vb  
Public Sub Main()  
  
    Dim myCounter As PerformanceCounter  
  
    Try  
        'Create the performance counter if it does not already exist.  
        If Not _  
        PerformanceCounterCategory.Exists("TaskExample") Then  
            PerformanceCounterCategory.Create("TaskExample", _  
                "Task Performance Counter Example", "Iterations", _  
                "Number of times this task has been called.")  
        End If  
  
        'Initialize the performance counter.  
        myCounter = New PerformanceCounter("TaskExample", _  
            "Iterations", String.Empty, False)  
  
        'Increment the performance counter.  
        myCounter.Increment()  
  
         myCounter.Close()  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Task Performance Counter Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
  
public class ScriptMain  
{  
  
public void Main()  
        {  
  
            PerformanceCounter myCounter;  
  
            try  
            {  
                //Create the performance counter if it does not already exist.  
                if (!PerformanceCounterCategory.Exists("TaskExample"))  
                {  
                    PerformanceCounterCategory.Create("TaskExample", "Task Performance Counter Example", "Iterations", "Number of times this task has been called.");  
                }  
  
                //Initialize the performance counter.  
                myCounter = new PerformanceCounter("TaskExample", "Iterations", String.Empty, false);  
  
                //Increment the performance counter.  
                myCounter.Increment();  
  
                myCounter.Close();  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Task Performance Counter Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
```  

