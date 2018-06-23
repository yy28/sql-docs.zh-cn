---
title: 配置检查点以重新启动失败的包 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3c2ae5affa24087bbb0511bc29559bba88f86cdb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126672"
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
  
    -   选择`IfExists`仅当检查点文件时，重新启动包。  
  
8.  配置包可以从中重新启动的任务和容器。  
  
    -   右键单击任务或容器，然后单击“属性”。  
  
    -   FailPackageOnFailure 属性设置为`True`每个所选任务和容器。  
  
## <a name="see-also"></a>请参阅  
 [通过使用检查点重启包](packages/restart-packages-by-using-checkpoints.md)  
  
  