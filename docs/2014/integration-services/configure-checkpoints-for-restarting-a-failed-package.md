---
title: 配置检查点以重新启动失败的包 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 220440313f0a06efb4ad55156a41fee18c61ab62
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376675"
---
# <a name="configure-checkpoints-for-restarting-a-failed-package"></a>配置检查点以重新启动失败的包
  通过设置应用于检查点的属性，可以将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包配置为从失败点重新启动，而不是重新运行整个包。  
  
### <a name="to-configure-a-package-to-restart"></a>将包配置为重新启动  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要配置的包所在的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在“解决方案资源管理器”中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  右键单击控制流设计图面背景中的任意位置，然后单击“属性”。  
  
5.  将 SaveCheckpoints 属性设置为`True`。  
  
6.  在 CheckpointFileName 属性中键入检查点文件的名称。  
  
7.  将 CheckpointUsage 属性设置为以下两个值之一：  
  
    -   选择 `Always`，始终从检查点重新启动包。  
  
        > [!IMPORTANT]  
        >  如果检查点文件不可用，将出现错误。  
  
    -   选择 `IfExists`，仅当检查文件可用时才重新启动包。  
  
8.  配置包可以从中重新启动的任务和容器。  
  
    -   右键单击任务或容器，然后单击“属性”。  
  
    -   将 FailPackageOnFailure 属性设置为`True`每个所选任务和容器。  
  
## <a name="see-also"></a>请参阅  
 [通过使用检查点重新启动包](packages/restart-packages-by-using-checkpoints.md)  
  
  
