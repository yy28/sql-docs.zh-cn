---
title: 文件系统任务编辑器（"常规" 页） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System Task Editor
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 594b87b3e2d58ffe60bd3c31324811a66038c82b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058805"
---
# <a name="file-system-task-editor-general-page"></a>文件系统任务编辑器（“常规”页）
  可以使用 **“文件系统任务编辑器”** 对话框的 **“常规”** 页，配置任务执行的文件系统操作。  
  
 若要了解此任务，请参阅 [File System Task](control-flow/file-system-task.md)。  
  
 必须通过设置 SourceConnection 和 DestinationConnection 属性来指定源和目标连接管理器。 您可以提供指向任务将其用作源或目标的文件的文件连接管理器的名称，如果文件路径存储在变量中，则可以提供变量的名称。 若要使用变量来存储文件路径，必须先将源连接的 IsSourcePathVariable 选项和目标连接的 IsDestinationPatheVariable 选项设置为 **True**。 然后，您可以选择使用现有的系统或用户定义变量，也可以创建新变量。 在 **“添加变量”** 对话框中，可以配置和指定变量的作用域。 该作用域必须是文件系统任务或父容器。 有关详细信息，请参阅[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)和[在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)。  
  
> [!NOTE]  
>  若要覆盖`SourceConnection`为和`DestinationConnection`属性选择的变量，请为 "**源**" 和 "**目标**" 属性输入表达式。 在 **“文件系统任务编辑器”** 的 **“表达式”** 页上输入表达式。 例如，若要设置任务作为目标的文件路径，您可能要在某些情况下使用变量 A 并在另一些情况下使用变量 B。  
  
> [!NOTE]  
>  文件系统任务对单个文件或目录进行操作。 因此，该任务不支持使用通配符对多个文件或目录执行同一操作。 若要使此文件系统任务对多个文件或目录重复执行某个操作，请将此文件系统任务放置于一个 Foreach 循环容器中。 有关详细信息，请参阅 [File System Task](control-flow/file-system-task.md)。  
  
 您可以使用表达式来使用不同的变量  
  
## <a name="options"></a>选项  
 **IsDestinationPathVariable**  
 指示目标路径是否存储在变量中。 此属性具有下表所列的选项。  
  
|Value|说明|  
|-----------|-----------------|  
|**True**|目标路径存储在变量中。 选择此值将显示动态选项 **DestinationVariable**。|  
|**False**|目标路径在文件连接管理器中指定。 选择此值将显示动态选项`DestinationConnection`。|  
  
 **OverwriteDestination**  
 指定操作是否可以覆盖目标目录中的文件。  
  
 **名称**  
 为文件系统任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **说明**  
 键入文件系统任务的说明。  
  
 **操作**  
 选择要执行的文件系统操作。 此属性具有下表所列的选项。  
  
|Value|说明|  
|-----------|-----------------|  
|**复制目录**|复制目录。 选择此值将显示源和目标的动态选项。|  
|**复制文件**|复制文件。 选择此值将显示源和目标的动态选项。|  
|**创建目录**|创建目录。 选择此值将显示源和目标目录的动态选项。|  
|**删除目录**|删除目录。 选择此值将显示源的动态选项。|  
|**删除目录内容**|删除目录的内容。 选择此值将显示源的动态选项。|  
|**删除文件**|删除文件。 选择此值将显示源的动态选项。|  
|**移动目录**|移动目录。 选择此值将显示源和目标的动态选项。|  
|**移动文件**|移动文件。 选择此值将显示源和目标的动态选项。<br /><br /> 注意：移动文件时，在作为目标提供的目录路径中不要包含文件名。|  
|**重命名文件**|重命名文件。 选择此值将显示源和目标的动态选项。<br /><br /> 注意：在重命名文件时，请在为目标提供的目录路径中包含新文件名。|  
|**设置属性**|设置文件或目录的属性。 选择此值将显示源和操作的动态选项。|  
  
 `IsSourcePathVariable`  
 指示目标路径是否存储在变量中。 此属性具有下表所列的选项。  
  
|Value||  
|-----------|-|  
|**True**|目标路径存储在变量中。 选择此值将显示动态选项 **SourceVariable**。|  
|**False**|目标路径在文件连接管理器中指定。 选择此值将显示动态选项 **DestinationVariable**。|  
  
## <a name="isdestinationpathvariable-dynamic-options"></a>IsDestinationPathVariable 动态选项  
  
### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 在列表中选择变量名称，或单击“\<新建变量...>”，创建一个新变量****。  
  
 **相关主题：** [Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 `DestinationConnection`  
 在列表中选择一个文件连接管理器，或\<单击 "**新建连接 ...** "> 创建新的连接管理器。  
  
 **相关主题：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="issourcepathvariable-dynamic-options"></a>IsSourcePathVariable 动态选项  
  
### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 在列表中选择变量名称，或单击“\<新建变量...>”，创建一个新变量****。  
  
 **相关主题：** [Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 `SourceConnection`  
 在列表中选择一个文件连接管理器，或\<单击 "**新建连接 ...** "> 创建新的连接管理器。  
  
 **相关主题：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="operation-dynamic-options"></a>Operation 动态选项  
  
### <a name="operation--set-attributes"></a>Operation = 设置属性  
 **Hidden**  
 指示文件或目录是否可见。  
  
 **只读**  
 指示文件是否是只读的。  
  
 **Archive**  
 指示文件或目录可以用于存档。  
  
 **系统**  
 指示文件是否是操作系统文件。  
  
### <a name="operation--create-directory"></a>Operation = 创建目录  
 `UseDirectoryIfExists`  
 指示“创建目录”操作是否使用具有指定名称的现有目录，而不创建新目录。****  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
