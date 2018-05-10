---
title: 脚本任务示例 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting-task-examples
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], examples
- examples [Integration Services]
- SSIS Script task, examples
ms.assetid: b0dd77ee-ee11-4cd9-87aa-61dd67f2fe1c
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cb4f0d3edbcab24dbd40d3a552c57d0cbaeb84a6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="script-task-examples"></a>脚本任务示例
  脚本任务是一个多用途工具，您可以在包中使用该工具以满足 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 附带的任务无法满足的几乎所有要求。 本主题列出了用于演示一些可用功能的脚本任务代码示例。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以这些脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
### <a name="example-topics"></a>示例主题  
 本节包含一些代码示例，这些示例演示了 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 类的各种用法，您可以将这些类并入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 脚本任务中。  
  
 [使用脚本任务检测空平面文件](../../integration-services/extending-packages-scripting-task-examples/detecting-an-empty-flat-file-with-the-script-task.md)  
 检查平面文件以确定该文件是否包含数据行，并将结果保存到变量以用于控制流分支。  
  
 [使用脚本任务为 ForEach 循环收集列表](../../integration-services/extending-packages-scripting-task-examples/gathering-a-list-for-the-foreach-loop-with-the-script-task.md)  
 收集满足用户指定条件的文件的列表，并填充变量以供 Foreach 源变量枚举器将来使用。  
  
 [使用脚本任务查询 Active Directory](../../integration-services/extending-packages-scripting-task-examples/querying-the-active-directory-with-the-script-task.md)  
 使用 System.DirectoryServices 命名空间中的类，基于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 变量的值从 Active Directory 检索用户信息。  
  
 [使用脚本任务监视性能计数器](../../integration-services/extending-packages-scripting-task-examples/monitoring-performance-counters-with-the-script-task.md)  
 使用 System.Diagnostics 命名空间中的类，创建可用于跟踪 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的执行进度的自定义性能计数器。  
  
 [使用脚本任务处理图像](../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)  
 使用 System.Drawing 命名空间中的类，将图像压缩为 JPEG 格式，并根据这些图像创建缩略图。  
  
 [使用脚本任务查找已安装的打印机](../../integration-services/extending-packages-scripting-task-examples/finding-installed-printers-with-the-script-task.md)  
 使用 Drawing.Printing 命名空间中的类，查找支持特定纸张大小的已安装打印机。  
  
 [使用脚本任务发送 HTML 邮件消息](../../integration-services/extending-packages-scripting-task-examples/sending-an-html-mail-message-with-the-script-task.md)  
 以 HTML 格式而不是纯文本格式发送邮件消息。  
  
 [使用脚本任务处理 Excel 文件](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
 列出了 Excel 文件中的工作表，并检查特定工作表是否存在。  
  
 [使用脚本任务向远程私有消息队列发送消息](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)  
 向远程私有消息队列发送消息。  
  
### <a name="other-examples"></a>其他示例  
 下面的主题还包含用于脚本任务的代码示例：  
  
 [在脚本任务中使用变量](../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 要求用户基于可能超出在另一个变量中指定的限制的包变量值，确认包是否应该继续运行。  
  
 [在脚本任务中连接数据源](../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 从在包中定义的连接管理器中检索连接或连接信息。  
  
 [在脚本任务中引发事件](../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 基于服务器上的 Internet 连接状态引发错误、警告或信息性消息。  
  
 [脚本任务中的日志记录](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 向已启用的日志提供程序记录由任务处理的项数。  
  
  
