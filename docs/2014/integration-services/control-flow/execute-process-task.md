---
title: 执行进程任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6b50470b6b12226cc14a837331b45ed0e16e4cfd
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366829"
---
# <a name="execute-process-task"></a>执行进程任务
  执行进程任务在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包工作流中运行应用程序或批处理文件。 虽然可以使用执行进程任务打开任意标准应用程序（例如 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 或 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]），但通常还是使用它来运行针对数据源执行的业务应用程序或批处理文件。 例如，可以使用执行进程任务来展开一个压缩的文本文件。 然后，包可将该文本文件用作包中数据流的数据源。 再举一个例子，您可以使用执行进程任务运行生成日销售额报表的自定义 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 应用程序。 然后，可以将该报表附加到发送邮件任务，并将其转发给通讯组列表。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 还包含一些执行工作流操作的其他任务（如执行包）。 有关详细信息，请参阅 [Execute Package Task](execute-package-task.md)  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>执行进程任务可用的自定义日志项  
 下表列出了执行进程任务的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../performance/integration-services-ssis-logging.md)和[日志记录的自定义消息](../custom-messages-for-logging.md)。  
  
|日志项|Description|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|提供所配置任务要运行的进程的信息。<br /><br /> 写入两个日志条目。 一个日志条目包含有关任务所运行可执行文件的名称和位置的信息，另一个条目则记录从可执行文件退出的信息。|  
|`ExecuteProcessVariableRouting`|提供有关哪些变量被路由到可执行文件的输入和输出的信息。 将为 stdin（输入）、stdout（输出）和 stderr（错误输出）写入日志条目。|  
  
## <a name="configuration-of-the-execute-process-task"></a>执行进程任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [执行进程任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [执行进程任务编辑器（“进程”页）](../execute-process-task-editor-process-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="property-settings"></a>属性设置  
 当执行进程任务运行自定义应用程序时，该任务将通过以下一种或两种方法为该应用程序提供输入：  
  
-   在 **StandardInputVariable** 属性设置中指定的变量。 有关变量的详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)和[在包中使用变量](../use-variables-in-packages.md)。  
  
-   在 **Arguments** 属性设置中指定的参数。 （例如，如果该任务打开一个 Word 格式的文档，该参数就可指定该 .doc 文件的名称。）  
  
 若要在一个执行进程任务中向自定义应用程序传递多个参数，请使用空格将这些参数隔开。 参数中不能包含空格，否则该任务将不运行。 可以使用表达式将变量值作为参数传递。 在下面的示例中，表达式将两个变量值作为参数传递并使用空格将参数隔开：  
  
 `@variable1 + " " + @variable2`  
  
 可以使用表达式设置执行进程任务的各种属性。  
  
 当你使用**StandardInputVariable**属性配置执行进程任务以提供输入时，调用`Console.ReadLine`从应用程序来读取输入的方法。 有关详细信息，请参阅 [Console.ReadLine 方法](https://go.microsoft.com/fwlink/?LinkId=129201)类库中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 主题。  
  
 当使用 **Arguments** 属性配置执行进程任务以提供输入时，请执行下列步骤之一以获得参数：  
  
-   如果使用 Microsoft Visual Basic 编写应用程序，请设置 `My.Application.CommandLineArgs` 属性。 下面的示例设置 `My.Application.CommandLineArgs` 属性以检索两个参数：  
  
    ```  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     有关详细信息，请参阅 [参考中的](https://go.microsoft.com/fwlink/?LinkId=129200)My.Application.CommandLineArgs 属性 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 这一主题。  
  
-   如果使用 Microsoft Visual C# 编写该应用程序，请使用 `Main` 方法。  
  
     有关详细信息，请参阅 C# 编程指南中的 [命令行参数（C# 编程指南）](https://go.microsoft.com/fwlink/?LinkId=129406)这一主题。  
  
 执行进程任务还包括 **StandardOutputVariable** 和 **StandardErrorVariable** 属性，用来分别指定使用该应用程序的标准输出和错误输出的变量。  
  
 另外，您还可以配置执行进程任务来指定工作目录、超时期限或表示可执行文件成功运行的值。 您还可以对该任务进行配置，使其在可执行文件的返回代码与指示成功的值不匹配时或者在指定位置找不到可执行文件时失败。  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>执行进程任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)  
  
  
