---
title: "执行进程任务编辑器（“进程”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executeprocesstask.process.f1"
helpviewer_keywords: 
  - "执行进程任务编辑器"
ms.assetid: 0fc22406-e79b-47a4-a7e4-108d4ce6202f
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# 执行进程任务编辑器（“进程”页）
  可以使用 **“执行进程任务编辑器”** 对话框的 **“进程”** 页配置执行进程的选项。 这些选项包括要运行的可执行文件、该可执行文件的位置、命令提示符参数以及提供输入及捕获输出的变量。  
  
 若要了解此任务，请参阅 [Execute Process Task](../../integration-services/control-flow/execute-process-task.md)。  
  
## 选项  
 **RequireFullFileName**  
 指示在指定位置未找到可执行文件时该任务是否应失败。  
  
 **可执行文件**  
 键入要运行的可执行文件的名称。  
  
 **参数**  
 提供命令提示符参数。  
  
 **WorkingDirectory**  
 键入包含可执行文件的文件夹的路径，或单击浏览 **(…)** 按钮定位到该文件夹。  
  
 **StandardInputVariable**  
 选择为进程提供输入的变量，或单击“\<新建变量...>”创建新的变量：  
  
 **相关主题：**[添加变量](../Topic/Add%20Variable.md)  
  
 **StandardOutputVariable**  
 选择捕获进程输出的变量，或单击“\<新建变量...>”创建新的变量。  
  
 **StandardErrorVariable**  
 选择捕获进程错误输出的变量，或单击“\<新建变量...>”创建新的变量。  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 指示在进程退出代码与 **SuccessValue** 中指定的值不同时任务是否失败。  
  
 **SuccessValue**  
 指定可执行文件返回的用来指示进程成功的值。 默认情况下，此值设置为 **0**。  
  
 **TimeOut**  
 指定进程可以运行的秒数。 如果值为 **0**，则表示不使用超时值，进程一直运行到处理完毕或出错为止。  
  
 **TerminateProcessAfterTimeOut**  
 指示在 **TimeOut** 选项指定的超时期限过后是否强制结束进程。 只有在 **TimeOut** 不为 **0**时，此选项才可用。  
  
 **WindowStyle**  
 指定用于运行进程的窗口样式。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
  