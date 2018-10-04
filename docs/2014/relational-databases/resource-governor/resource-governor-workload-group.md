---
title: 资源调控器工作负荷组 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group
- workload groups [SQL Server]
- workload groups [SQL Server], overview
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6e92db2f26a53ac52b905dd7c8352111f2a88451
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179617"
---
# <a name="resource-governor-workload-group"></a>资源调控器工作负荷组
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源调控器中，工作负荷组充当具有相似分类标准的会话请求的容器。 工作负荷允许对会话进行聚合监视，并定义会话的策略。 每个工作负荷组均位于一个资源池中，它表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的部分物理资源。 在某个会话启动时，资源调控器分类器会将此会话分配给一个特定的工作负荷组，并且此会话必须使用分配给该工作负荷组的策略和为资源池定义的资源运行。  
  
## <a name="workload-group-concepts"></a>工作负荷组概念  
 工作负荷组是会话请求的容器，根据应用于每个请求的分类标准这些会话被认为是相似的。 利用工作负荷组可对资源占用进行聚合监视并可将统一策略应用至组中的所有请求。 组为其成员定义策略。  
  
> [!NOTE]  
>  用户定义的工作负荷组可以从一个资源池移动到另一个资源池。  
  
 资源调控器预定义了两个工作负荷组：内部组和默认组。 用户无法更改任何已归入内部组类的请求，但可以对其进行监视。 当满足下列条件时，请求会被归入默认组类：  
  
-   没有用于对请求进行分类的标准。  
  
-   曾经尝试将请求归入不存在的组类。  
  
-   存在常规性的分类错误。  
  
 资源调控器还提供了用于创建、更改和删除工作负荷组的 DDL 语句。  
  
## <a name="workload-group-tasks"></a>工作负荷组任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|说明如何创建工作负荷组。|[创建工作负荷组](create-a-workload-group.md)|  
|说明如何更改工作负荷组设置。|[更改工作负荷组设置](change-workload-group-settings.md)|  
|说明如何删除工作负荷组。|[删除工作负荷组](delete-a-workload-group.md)|  
  
## <a name="see-also"></a>请参阅  
 [资源调控器](resource-governor.md)   
 [启用资源调控器](enable-resource-governor.md)   
 [资源调控器资源池](resource-governor-resource-pool.md)   
 [资源调控器分类器函数](resource-governor-classifier-function.md)   
 [使用模板配置资源调控器](configure-resource-governor-using-a-template.md)   
 [查看资源调控器属性](view-resource-governor-properties.md)  
  
  
