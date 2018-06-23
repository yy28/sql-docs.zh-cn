---
title: 任务 8： 创建复合域规则 |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 18461e889e56f647b869d2b60cae49d662786160
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129805"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>任务 8：创建复合域规则
  在此任务中，你创建的规则**地址验证**复合域。 定义跨域规则： 如果**城市**是**洛杉矶**，**状态**必须**CA**其中**城市**和**状态**了两个域。  
  
1.  在右窗格中，切换到**CD 规则**选项卡。  
  
2.  单击**添加新的域规则**从工具栏中。  
  
3.  类型**城邦规则**为**名称**按**ENTER**。  
  
4.  在**生成规则**窗格中，选择**城市**在域列表中，选择条件**值等于**和类型**洛杉矶**为值。  
  
5.  在**然后**窗格中，选择**状态**域列表中，然后选择**值等于**，类型**CA**值，然后按**选项卡**。  
  
     ![复合域规则](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "复合域规则")  
  
6.  单击**关闭**页后，可以切换到 DQS 客户端的主页面底部的按钮。 在下一课将发布知识库。 注意，知识库处于锁定状态（锁定图标）。  
  
## <a name="next-step"></a>下一步  
 [任务 9：配置引用数据服务](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  