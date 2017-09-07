---
title: "脚本任务中的日志记录 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- logs [Integration Services], scripts
- Integration Services packages, logs
- Log method
- SSIS Script task, logs
- Script task [Integration Services], logs
- packages [Integration Services], logs
ms.assetid: 2e11fc15-df18-4309-bd2d-fc58aa4b9b7a
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 98859dafe0b023954f10239fe11e8b76f36ab28b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-task"></a>脚本任务中的日志记录
  使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包中的日志记录可以记录预定义的事件或用户定义的消息，从而记录有关执行进度、结果和问题的详细信息，供随后分析时使用。 可以使用脚本任务<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>方法**Dts**对象来记录用户定义数据。 如果启用日志记录，和**ScriptTaskLogEntry**来登录选择事件**详细信息**选项卡**配置 SSIS 日志**对话框中，一次对<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>方法将事件信息存储在为该任务配置的所有日志提供程序。  
  
> [!NOTE]  
>  尽管可以直接从脚本任务执行日志记录，但是您可能希望考虑实现事件，而不是日志记录。 如果使用事件，不仅能够启用事件消息的日志记录，而且能够通过默认或用户定义的事件处理程序响应事件。  
  
 有关日志记录的详细信息，请参阅[Integration Services &#40;SSIS &#41;日志记录](../../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="logging-example"></a>日志记录示例  
 下面的示例演示通过记录表示已处理的行数的值，从脚本任务进行日志记录。  
  
```vb  
Public Sub Main()  
  
    Dim rowsProcessed As Integer = 100  
    Dim emptyBytes(0) As Byte  
  
    Try  
        Dts.Log("Rows processed: " & rowsProcessed.ToString, _  
            0, _  
            emptyBytes)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
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
            //  
            int rowsProcessed = 100;  
            byte[] emptyBytes = new byte[0];  
  
            try  
            {  
                Dts.Log("Rows processed: " + rowsProcessed.ToString(), 0, emptyBytes);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                //An error occurred.  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
```  
  
 }  
  
## <a name="external-resources"></a>外部资源  
  
-   博客文章[记录为 Integration Services 任务的自定义事件](http://go.microsoft.com/fwlink/?LinkId=165644)，dougbert.com 上  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS &#41;日志记录](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
