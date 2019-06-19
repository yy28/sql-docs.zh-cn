---
title: Hadoop Pig 任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4991fd3ad95a633881099b9677c9db55935f6a13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727601"
---
# <a name="hadoop-pig-task"></a>Hadoop Pig 任务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用 Hadoop Pig 任务可以在 Hadoop 群集上运行 Pig 脚本。  
  
 要添加 Hadoop Pig 任务，请将其拖放到设计器。 然后双击该任务，或右键单击，然后单击“编辑”  ，以打开“Hadoop Pig 任务编辑器”  对话框。  
  
 ![Hadoop Pig 任务编辑器](../../integration-services/control-flow/media/hadoop-pig-task.png "Hadoop Pig Task Editor")  
  
## <a name="options"></a>选项  
 在“Hadoop Pig 任务编辑器”对话框  中配置下列选项。  
  
|字段|描述|  
|-----------|-----------------|  
|**Hadoop 连接**|指定现有的一个 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明 WebHCat 服务的托管位置。|  
|**SourceType**|指定该查询的源类型。 可用的值为“ScriptFile”  和“DirectInput”  。|  
|**InlineScript**|当“SourceType”  的值为“DirectInput”  时，指定 Pig 脚本。|  
|**HadoopScriptFilePath**|当“SourceType”  的值为“ScriptFile”  时，在 Hadoop 上指定脚本文件路径。|  
|**TimeoutInMinutes**|指定超时值（以分钟为单位）。 如果 Hadoop 作业在超时已过之前未完成，则该作业停止。 指定 0 则计划以异步方式运行 Hadoop 作业。|  
  
## <a name="see-also"></a>另请参阅  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
