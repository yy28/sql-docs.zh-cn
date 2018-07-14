---
title: 查看发布服务器的信息和执行其任务（复制监视器）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Publishers [SQL Server replication], Replication Monitor tasks
- viewing Publisher information
- Publishers [SQL Server replication], viewing information
ms.assetid: 1e777e95-377a-4de3-b965-867464aadaaf
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99368187a8edbc829098ff723f30c2b14d10051c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177644"
---
# <a name="view-information-and-perform-tasks-for-a-publisher-replication-monitor"></a>查看发布服务器的信息和执行其任务（复制监视器）
  复制监视器提供了下列选项卡，以显示有关选定发布服务器的信息：  
  
-   **发布**  
  
     此选项卡显示选定发布服务器上所有发布的相关信息。  
  
-   **订阅监视列表**  
  
     此选项卡用于显示所选发布服务器上所有可用发布的订阅的信息：有错误、出现警告或性能最差。 对于运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]以前版本的分发服务器，不显示此选项卡。  
  
-   **“代理”** 选项卡  
  
     此选项卡显示所有类型的复制所使用的代理和作业的详细信息。 使用该选项卡，还可以启动和停止每个代理和作业。  
  
 若要查看每个选项卡上各个选项的详细信息，请在右窗格中单击该选项卡，再单击菜单栏上的 **“帮助”** 。 有关启动复制监视器的信息，请参阅[启动复制监视器](start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-a-publisher"></a>查看发布服务器的信息和执行其任务  
  
1.  在左窗格中，展开发布服务器组，然后单击一个发布服务器。  
  
2.  若要查看所有发布的信息，请单击 **“发布”** 选项卡。  
  
3.  若要查看有关订阅的信息，请单击 **“订阅监视列表”** 选项卡。还可以从此访问更详细的信息以及执行任务：  
  
    -   若要查看与订阅相关联的代理的详细信息，请右键单击该订阅，再单击 **“查看详细信息”**。  
  
    -   若要查看订阅的属性，请右键单击该订阅，然后单击 **“属性”**。  
  
    -   若要同步推送订阅，请右键单击该订阅，然后单击 **“开始同步”**。  
  
    -   若要重新初始化订阅，请右键单击该订阅，然后单击 **“重新初始化订阅”**。  
  
4.  若要查看有关代理的信息，请单击 **“代理”** 选项卡。您还可以通过此选项卡访问更详细的信息并执行任务：  
  
    -   若要查看有关代理的详细信息（如信息性消息以及任何错误消息），请右键单击代理，然后单击 **“查看详细信息”**。  
  
    -   若要查看有关运行代理的作业的详细信息（如计划、作业步骤详细信息等等），请右键单击代理，然后单击 **“属性”**。  
  
    -   若要管理代理的配置文件，请右键单击代理，然后单击 **“代理配置文件”**。 有关详细信息，请参阅[处理复制代理配置文件](../agents/replication-agent-profiles.md)。  
  
    -   若要启动未运行的代理，请右键单击代理，然后单击 **“启动代理”**。  
  
    -   若要停止运行中的代理，请右键单击代理，然后单击 **“停止代理”**。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改分发服务器和发布服务器属性](../view-and-modify-distributor-and-publisher-properties.md)   
 [监视复制](../monitoring-replication.md)  
  
  
