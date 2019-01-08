---
title: 维护计划（服务器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.maintplanproperties.server.f1
- sql12.swb.maint.servers.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 989b2992407c4a3825d42106d848598a723a41c5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747659"
---
# <a name="maintenance-plan-servers"></a>维护计划（服务器）
  使用 **“服务器”** 对话框可以选择要在其上运行维护计划的服务器。  
  
 必须配置包含一台主服务器和一台或多台目标服务器的多服务器环境，才能创建多服务器维护计划。 在多服务器维护计划中，应将本地服务器配置为主服务器。 在多服务器环境中，此对话框显示 **(local)** 主服务器和所有相应的目标服务器。 将为本地服务器创建一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。 此功能是处于启用还是禁用状态，取决于你是否选择了 **(local)** 服务器。 如果选择了目标服务器，将创建一个多服务器作业，并且该作业将下载到每个选定的目标服务器上。 如果未选择任何目标服务器，则会删除该多服务器作业。  
  
## <a name="see-also"></a>请参阅  
 [维护计划](maintenance-plans.md)   
 [创建多服务器环境](../../ssms/agent/create-a-multiserver-environment.md)   
 [设置主服务器](../../ssms/agent/make-a-master-server.md)   
 [设置目标服务器](../../ssms/agent/make-a-target-server.md)  
  
  
