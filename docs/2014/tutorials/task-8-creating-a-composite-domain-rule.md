---
title: 任务 8:创建复合域规则 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c17508b14ba8352e8dd17e2e0c1322c0c1856ed6
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156193"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>任务 8:创建复合域规则
  在此任务中，创建的规则**地址验证**复合域。 你可以定义跨域规则： 如果**城市**是**Los Angeles**，**状态**必须是**CA**其中**城市**并**状态**是两个域。  
  
1.  在右窗格中，切换到**复合域规则**选项卡。  
  
2.  单击**添加新的域规则**从工具栏中。  
  
3.  类型**城市-州规则**有关**名称**然后按**ENTER**。  
  
4.  中**生成规则**窗格中，选择**市/县**在域列表中，然后选择条件**值等于**并键入**Los Angeles**为值。  
  
5.  在中**然后**窗格中，选择**状态**域列表中，然后选择**值等于**，类型**CA**值，然后按**选项卡**。  
  
     ![复合域规则](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "复合域规则")  
  
6.  单击**关闭**页后，可以切换到 DQS 客户端的主页面底部的按钮。 在下一课将发布知识库。 注意，知识库处于锁定状态（锁定图标）。  
  
## <a name="next-step"></a>下一步  
 [任务 9:配置引用数据服务](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  
