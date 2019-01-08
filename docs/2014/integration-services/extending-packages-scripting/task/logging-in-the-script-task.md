---
title: 脚本任务中的日志记录 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c46528a51f8dae36b2b47afe2086a6eac1b72428
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359499"
---
# <a name="logging-in-the-script-task"></a>脚本任务中的日志记录
  使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包中的日志记录可以记录预定义的事件或用户定义的消息，从而记录有关执行进度、结果和问题的详细信息，供随后分析时使用。 脚本任务可以使用 `Dts` 对象的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 方法记录用户定义的数据。 如果启用了日志记录，并且在“配置 SSIS 日志”对话框的“详细信息”选项卡中为日志记录选择了 ScriptTaskLogEntry 事件，则调用一次 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 方法即可将事件信息存储在为该任务配置的所有日志提供程序中。  
  
> [!NOTE]  
>  尽管可以直接从脚本任务执行日志记录，但是您可能希望考虑实现事件，而不是日志记录。 如果使用事件，不仅能够启用事件消息的日志记录，而且能够通过默认或用户定义的事件处理程序响应事件。  
  
 有关日志记录的详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../performance/integration-services-ssis-logging.md)。  
  
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
  
-   dougbert.com 上的博客文章 [为 Integration Services 任务记录自定义事件](https://go.microsoft.com/fwlink/?LinkId=165644)  
  
![集成服务图标 （小）](../../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 日志记录](../../performance/integration-services-ssis-logging.md)  
  
  
