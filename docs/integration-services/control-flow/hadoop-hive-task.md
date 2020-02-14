---
title: Hadoop Hive 任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoophivetask.f1
ms.assetid: 10ff37c0-9f3f-442a-889b-c351afbdc74c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f157b2b802142f6f00b7a3e9ffb2596ef80f1773
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298261"
---
# <a name="hadoop-hive-task"></a>Hadoop 配置单元任务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用 Hadoop 配置单元任务可以在 Hadoop 群集上运行配置单元脚本。  
  
 要添加 Hadoop 配置单元任务，请将其拖放到设计器。 然后双击该任务，或右键单击，然后单击“编辑”  ，以打开“Hadoop 配置单元任务编辑器”  对话框。  
  
 ![Hadoop Hive 任务编辑器](../../integration-services/control-flow/media/hadoop-hive-task.png "Hadoop Hive 任务编辑器")  
  
## <a name="options"></a>选项  
 配置“Hadoop 配置单元任务编辑器”对话框  中的下列选项。  
  
|字段|说明|  
|-----------|-----------------|  
|**Hadoop 连接**|指定现有的一个 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明 WebHCat 服务的托管位置。|  
|**SourceType**|指定该查询的源类型。 可用的值为“ScriptFile”  和“DirectInput”  。|  
|**InlineScript**|当 **“SourceType”** 的值为“DirectInput”  时，指定配置单元脚本。|  
|**HadoopScriptFilePath**|当“SourceType”  的值为“ScriptFile”  时，在 Hadoop 上指定脚本文件路径。|  
|**TimeoutInMinutes**|指定超时值（以分钟为单位）。 如果 Hadoop 作业在超时已过之前未完成，则该作业停止。 指定 0 则计划以异步方式运行 Hadoop 作业。|  
  
## <a name="see-also"></a>另请参阅  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
