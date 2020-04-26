---
title: 任务8：创建复合域规则 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7e40ec982a9b2c43c3d55ec60179ac9a0b80e8a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489632"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>任务 8：创建复合域规则
  在此任务中，您将为 "**地址验证**" 复合域创建规则。 定义跨域规则：如果**city**为**洛杉矶，则** **state**必须为**CA** ，其中**City**和**state**是两个域。  
  
1.  在右侧窗格中，切换到 " **CD 规则**" 选项卡。  
  
2.  单击工具栏中的 "**添加新的域规则**"。  
  
3.  键入 " **City-** **Name**规则"，然后按**enter**。  
  
4.  在 "**生成规则**" 窗格中，选择 "域列表" 中的 "**城市**"，然后选择 "条件**值等于**"，然后键入**洛杉矶**作为值。  
  
5.  在 " **Then** " 窗格中，选择 "域列表" 中的 "**状态**"，然后选择 "**值等于**"，键入**CA**作为值，然后按**tab**。  
  
     ![复合域规则](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "复合域规则")  
  
6.  单击页面底部的 "**关闭**" 按钮可切换到 DQS 客户端的主页。 在下一课将发布知识库。 注意，知识库处于锁定状态（锁定图标）。  
  
## <a name="next-step"></a>下一步  
 [任务 9：配置引用数据服务](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  
