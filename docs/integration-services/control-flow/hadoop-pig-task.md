---
title: Hadoop Pig 任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2d1fd71578a1f9f6a9bee87ac54adbfeaa1305aa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="hadoop-pig-task"></a>Hadoop Pig 任务
  使用 Hadoop Pig 任务可以在 Hadoop 群集上运行 Pig 脚本。  
  
 要添加 Hadoop Pig 任务，请将其拖放到设计器。 然后双击该任务，或右键单击，然后单击“编辑”，以打开“Hadoop Pig 任务编辑器”对话框。  
  
 ![Hadoop Pig 任务编辑器](../../integration-services/control-flow/media/hadoop-pig-task.png "Hadoop Pig Task Editor")  
  
## <a name="options"></a>“常规”  
 在“Hadoop Pig 任务编辑器”对话框  中配置下列选项。  
  
|字段|Description|  
|-----------|-----------------|  
|**Hadoop 连接**|指定现有的一个 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明 WebHCat 服务的托管位置。|  
|**SourceType**|指定该查询的源类型。 可用的值为“ScriptFile”  和“DirectInput” 。|  
|**InlineScript**|当“SourceType”  的值为“DirectInput” 时，指定 Pig 脚本。|  
|**HadoopScriptFilePath**|当“SourceType”  的值为“ScriptFile” 时，在 Hadoop 上指定脚本文件路径。|  
|**TimeoutInMinutes**|指定超时值（以分钟为单位）。 如果 Hadoop 作业在超时已过之前未完成，则该作业停止。 指定 0 则计划以异步方式运行 Hadoop 作业。|  
  
## <a name="see-also"></a>另请参阅  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
