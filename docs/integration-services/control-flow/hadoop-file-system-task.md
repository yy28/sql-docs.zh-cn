---
title: Hadoop 文件系统任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e97ae33bcccee338be576138ca335bd6298e0128
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294069"
---
# <a name="hadoop-file-system-task"></a>Hadoop 文件系统任务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Hadoop 文件系统任务允许 SSIS 包在 Hadoop 群集之间或内部复制文件。  
  
 要添加 Hadoop 文件系统任务，请将其拖放到设计器。 然后双击该任务，或右键单击，然后单击“编辑”，以打开“Hadoop 文件系统任务编辑器”对话框。    
  
 ![Hadoop 文件系统任务编辑器](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Hadoop 文件系统任务编辑器")  
  
## <a name="options"></a>选项  
 配置“Hadoop 文件系统任务编辑器”对话框  中的下列选项。  
  
|字段|说明|  
|-----------|-----------------|  
|**Hadoop 连接**|指定现有的一个 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明目标文件的托管位置。|  
|**Hadoop 文件路径**|指定 HDFS 上的文件或目录路径。|  
|**Hadoop 文件类型**|指定 HDFS 文件系统对象是文件还是目录。|  
|**覆盖目标**|如果目标文件已经存在，则指定是否将其覆盖。|  
|**操作**|指定运算。 可用运算是 **CopyToHDFS**、 **CopyFromHDFS**和 **CopyWithinHDFS**。|  
|**本地文件连接**|指定一个现有的文件连接管理器，或新建一个文件连接管理器。 此连接管理器指明源文件的托管位置。|  
|**递归**|指定是否要以递归方式复制所有子文件夹。|  
  
## <a name="see-also"></a>另请参阅  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [文件连接管理器](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
