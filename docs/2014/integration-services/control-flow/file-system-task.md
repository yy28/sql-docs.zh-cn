---
title: 文件系统任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cd924464331b144040f33797d0333b1ddb5a4032
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790939"
---
# <a name="file-system-task"></a>文件系统任务
  文件系统任务对文件系统中的文件和目录执行操作。 例如，通过使用文件系统任务，包可以创建、移动或删除目录和文件。 您还可以使用文件系统任务设置文件和目录的属性。 例如，文件系统任务可以让文件隐藏或只读。  
  
 所有文件系统任务操作都使用源，源可以是文件或目录。 例如，任务复制的文件或删除的目录都是源。 源可以通过使用指向目录或文件的文件连接管理器来指定，也可以通过提供包含源路径的变量的名称来指定。 有关详细信息，请参阅[文件连接管理器](../connection-manager/file-connection-manager.md)和 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)。  
  
 复制和移动文件及目录的操作与重命名文件的操作都使用目标和源。 目标可以使用文件连接管理器或变量指定。 文件系统任务操作可以配置为允许覆盖目标文件和目录。 创建新目录的操作可以配置为使用具有指定名称的现有目录，而不是在目录已经存在时失败。  
  
## <a name="predefined-file-system-operations"></a>预定义的文件系统操作  
 文件系统任务包含一组预定义的操作。 下表介绍了这些运算。  
  
|操作|Description|  
|---------------|-----------------|  
|复制目录|将文件夹从一个位置复制到另一个位置。|  
|复制文件|将文件从一个位置复制到另一个位置。|  
|创建目录|在指定位置创建文件夹。|  
|删除目录|删除指定位置的文件夹。|  
|删除目录内容|删除文件夹中的所有文件和文件夹。|  
|删除文件|删除指定位置的文件。|  
|移动目录|将文件夹从一个位置移动到另一个位置。|  
|移动文件|将文件从一个位置移动到另一个位置。|  
|重命名文件|重命名指定位置的文件。|  
|设置属性|设置文件和文件夹的属性。 属性包括“存档”、“隐藏”、“正常”、“只读”和“系统”。 “正常”指没有属性，它不能与其他属性结合使用。 所有其他属性都可以组合使用。|  
  
 文件系统任务对单个文件或目录进行操作。 因此，该任务不支持使用通配符对多个文件执行相同的操作。 若要使此文件系统任务对多个文件或目录重复执行某个操作，请将此文件系统任务放置于一个 Foreach 循环容器中，如下面的步骤所述：  
  
-   **配置 Foreach 循环容器** 在 Foreach 循环编辑器的 **“集合”** 页上，将枚举器设置为 **“Foreach 文件枚举器”** ，然后输入通配符表达式作为 **“文件”** 的枚举器配置。 在 Foreach 循环编辑器的 **“变量映射”** 页上，将要用来传递文件名称的变量按照一次一个的方式映射至文件系统任务。  
  
-   **添加和配置文件系统任务** 将文件系统任务添加到 Foreach 循环容器。 在文件系统任务编辑器的 **“常规”** 页上，将 **“SourceVariable”** 或 **“DestinationVariable”** 属性设置为您在 Foreach 循环容器中定义的变量。  
  
## <a name="custom-log-entries-available-on-the-file-system-task"></a>文件系统任务可用的自定义日志项  
 下表介绍了文件系统任务的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../performance/integration-services-ssis-logging.md)和[日志记录的自定义消息](../custom-messages-for-logging.md)。  
  
|日志项|Description|  
|---------------|-----------------|  
|`FileSystemOperation`|报告任务所执行的操作。 在文件系统操作开始时写入日志项，日志项包括有关源和目标的信息。|  
  
## <a name="configuring-the-file-system-task"></a>配置文件系统任务  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅以下主题：  
  
-   [文件系统任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请参阅以下主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
 有关如何以编程方式设置这些属性的详细信息，请参阅以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括一个可下载和上载数据文件以及管理服务器上目录的任务。 有关详细信息，请参阅 [FTP Task](ftp-task.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)  
  
  
