---
title: Hadoop 文件系统任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b963428b347e86b10f8110b21c95b32f1c10eea0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="hadoop-file-system-task"></a>Hadoop 文件系统任务
  Hadoop 文件系统任务允许 SSIS 包在 Hadoop 群集之间或内部复制文件。  
  
 要添加 Hadoop 文件系统任务，请将其拖放到设计器。 然后双击该任务，或右键单击，然后单击“编辑”，以打开“Hadoop 文件系统任务编辑器”对话框。  
  
 ![Hadoop 文件系统任务编辑器](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Hadoop File System Task Editor")  
  
## <a name="options"></a>“常规”  
 配置“Hadoop 文件系统任务编辑器”对话框  中的下列选项。  
  
|字段|Description|  
|-----------|-----------------|  
|**Hadoop 连接**|指定现有的一个 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明目标文件的托管位置。|  
|**Hadoop 文件路径**|指定 HDFS 上的文件或目录路径。|  
|**Hadoop 文件类型**|指定 HDFS 文件系统对象是文件还是目录。|  
|**覆盖目标**|如果目标文件已经存在，则指定是否将其覆盖。|  
|**运算**|指定运算。 可用运算是 **CopyToHDFS**、 **CopyFromHDFS**和 **CopyWithinHDFS**。|  
|**本地文件连接**|指定一个现有的文件连接管理器，或新建一个文件连接管理器。 此连接管理器指明源文件的托管位置。|  
|**递归**|指定是否要以递归方式复制所有子文件夹。|  
  
## <a name="see-also"></a>另请参阅  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [文件连接管理器](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
