---
title: "Hadoop Pig 任务 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 816ca947c45128a996686d1269815ac909e364fe
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="hadoop-pig-task"></a>Hadoop Pig 任务
  使用 Hadoop Pig 任务可以在 Hadoop 群集上运行 Pig 脚本。  
  
 要添加 Hadoop Pig 任务，请将其拖放到设计器。 然后双击该任务，或右键单击，然后单击“编辑”，以打开“Hadoop Pig 任务编辑器”对话框。  
  
 ![Hadoop Pig 任务编辑器](../../integration-services/control-flow/media/hadoop-pig-task.png "Hadoop Pig 任务编辑器")  
  
## <a name="options"></a>选项  
 在“Hadoop Pig 任务编辑器”对话框  中配置下列选项。  
  
|字段|Description|  
|-----------|-----------------|  
|**Hadoop 连接**|指定一个现有的 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明 WebHCat 服务的托管位置。|  
|**SourceType**|指定该查询的源类型。 可用的值为“ScriptFile”  和“DirectInput” 。|  
|**InlineScript**|当“SourceType”  的值为“DirectInput” 时，指定 Pig 脚本。|  
|**HadoopScriptFilePath**|当“SourceType”  的值为“ScriptFile” 时，在 Hadoop 上指定脚本文件路径。|  
|**TimeoutInMinutes**|指定超时值（以分钟为单位）。 如果 Hadoop 作业在超时已过之前未完成，则该作业停止。 指定 0 则计划以异步方式运行 Hadoop 作业。|  
  
## <a name="see-also"></a>另请参阅  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
