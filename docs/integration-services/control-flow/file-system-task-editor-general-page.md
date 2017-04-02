---
title: "文件系统任务编辑器（“常规”页） | Microsoft Docs"
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
  - "sql13.dts.designer.filesystemtask.general.f1"
helpviewer_keywords: 
  - "文件系统任务编辑器"
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# 文件系统任务编辑器（“常规”页）
  可以使用 **“文件系统任务编辑器”** 对话框的 **“常规”** 页，配置任务执行的文件系统操作。  
  
 若要了解此任务，请参阅 [File System Task](../../integration-services/control-flow/file-system-task.md)。  
  
 必须通过设置 SourceConnection 和 DestinationConnection 属性来指定源和目标连接管理器。 您可以提供指向任务将其用作源或目标的文件的文件连接管理器的名称，如果文件路径存储在变量中，则可以提供变量的名称。 若要使用变量来存储文件路径，必须先将源连接的 IsSourcePathVariable 选项和目标连接的 IsDestinationPatheVariable 选项设置为 **True**。 然后，您可以选择使用现有的系统或用户定义变量，也可以创建新变量。 在 **“添加变量”** 对话框中，可以配置和指定变量的作用域。 该作用域必须是文件系统任务或父容器。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](../Topic/Use%20Variables%20in%20Packages.md)。  
  
> [!NOTE]  
>  若要覆盖为 **SourceConnection** 和 **DestinationConnection** 属性选择的变量，请为 **“源”** 和 **“目标”** 属性输入表达式。 在 **“文件系统任务编辑器”** 的 **“表达式”**页上输入表达式。 例如，若要设置任务作为目标的文件路径，您可能要在某些情况下使用变量 A 并在另一些情况下使用变量 B。  
  
> [!NOTE]  
>  文件系统任务对单个文件或目录进行操作。 因此，该任务不支持使用通配符对多个文件或目录执行同一操作。 若要使此文件系统任务对多个文件或目录重复执行某个操作，请将此文件系统任务放置于一个 Foreach 循环容器中。 有关详细信息，请参阅 [File System Task](../../integration-services/control-flow/file-system-task.md)。  
  
 您可以使用表达式来使用不同的变量  
  
## 选项  
 **IsDestinationPathVariable**  
 指示目标路径是否存储在变量中。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**True**|目标路径存储在变量中。 选择此值将显示动态选项 **DestinationVariable**。|  
|**False**|目标路径在文件连接管理器中指定。 选择此值将显示动态选项 **DestinationConnection**。|  
  
 **OverwriteDestination**  
 指定操作是否可以覆盖目标目录中的文件。  
  
 **名称**  
 为文件系统任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **Description**  
 键入文件系统任务的说明。  
  
 **运算**  
 选择要执行的文件系统操作。 此属性具有下表所列的选项。  
  
|“值”|Description|  
|-----------|-----------------|  
|**复制目录**|复制目录。 选择此值将显示源和目标的动态选项。|  
|**复制文件**|复制文件。 选择此值将显示源和目标的动态选项。|  
|**创建目录**|创建目录。 选择此值将显示源和目标目录的动态选项。|  
|**删除目录**|删除目录。 选择此值将显示源的动态选项。|  
|**删除目录内容**|删除目录的内容。 选择此值将显示源的动态选项。|  
|**删除文件**|删除文件。 选择此值将显示源的动态选项。|  
|**移动目录**|移动目录。 选择此值将显示源和目标的动态选项。|  
|**移动文件**|移动文件。 选择此值将显示源和目标的动态选项。 移动文件时，在作为目标提供的目录路径中不要包含文件名。|  
|**重命名文件**|重命名文件。 选择此值将显示源和目标的动态选项。 重命名文件时，请在为目标提供的目录路径中包含新文件名。|  
|**设置属性**|设置文件或目录的属性。 选择此值将显示源和操作的动态选项。|  
  
 **IsSourcePathVariable**  
 指示目标路径是否存储在变量中。 此属性具有下表所列的选项。  
  
|“值”||  
|-----------|-|  
|**True**|目标路径存储在变量中。 选择此值将显示动态选项 **SourceVariable**。|  
|**False**|目标路径在文件连接管理器中指定。 选择此值将显示动态选项 **DestinationVariable**。|  
  
## IsDestinationPathVariable 动态选项  
  
### IsDestinationPathVariable = True  
 **DestinationVariable**  
 在列表中选择变量名称，或单击“\<新建变量...>”创建新变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](../Topic/Add%20Variable.md)  
  
### IsDestinationPathVariable = False  
 **DestinationConnection**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”新建一个连接管理器。  
  
 **相关主题：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## IsSourcePathVariable 动态选项  
  
### IsSourcePathVariable = True  
 **SourceVariable**  
 在列表中选择变量名称，或单击“\<新建变量...>”创建新变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](../Topic/Add%20Variable.md)  
  
### IsSourcePathVariable = False  
 **SourceConnection**  
 在列表中选择一个文件连接管理器，或单击“\<新建连接…>”新建一个连接管理器。  
  
 **相关主题：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## Operation 动态选项  
  
### Operation = 设置属性  
 **Hidden**  
 指示文件或目录是否可见。  
  
 **ReadOnly**  
 指示文件是否是只读的。  
  
 **Archive**  
 指示文件或目录可以用于存档。  
  
 **系统**  
 指示文件是否是操作系统文件。  
  
### Operation = 创建目录  
 **UseDirectoryIfExists**  
 指示“创建目录”操作是否使用具有指定名称的现有目录，而不创建新目录。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
  