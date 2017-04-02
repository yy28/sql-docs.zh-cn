---
title: "配置检查点以重新启动失败的包 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "检查点 [Integration Services]"
  - "重新启动包"
  - "启动包"
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# 配置检查点以重新启动失败的包
  通过设置应用于检查点的属性，可以将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包配置为从失败点重新启动，而不是重新运行整个包。  
  
### 将包配置为重新启动  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开要配置的包所在的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在“解决方案资源管理器”中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  右键单击控制流设计图面背景中的任意位置，然后单击“属性”。  
  
5.  将 SaveCheckpoints 属性设置为 **True**。  
  
6.  在 CheckpointFileName 属性中键入检查点文件的名称。  
  
7.  将 CheckpointUsage 属性设置为以下两个值之一：  
  
    -   选择 **Always** ，始终从检查点重新启动包。  
  
        > [!IMPORTANT]  
        >  如果检查点文件不可用，将出现错误。  
  
    -   选择 **IfExists** ，仅当检查文件可用时才重新启动包。  
  
8.  配置包可以从中重新启动的任务和容器。  
  
    -   右键单击任务或容器，然后单击“属性”。  
  
    -   将每个所选任务和容器的 FailPackageOnFailure 属性设置为 **True**。  
  
## 另请参阅  
 [通过使用检查点重新启动包](../../integration-services/packages/restart-packages-by-using-checkpoints.md)  
  
  