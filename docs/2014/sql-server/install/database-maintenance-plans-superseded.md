---
title: 数据库维护计划被取代 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- suspended database maintenance plans
- database maintenance plans [SQL Server Agent]
- maintenance plans [SQL Server Agent]
ms.assetid: efac127c-6c81-4c7a-a6c4-9aae5d15545d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d41763582632a92b3a38bdbd67ee55b65f95b6d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095761"
---
# <a name="database-maintenance-plans-superseded"></a>数据库维护计划被取代
    
## <a name="component"></a>组件  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理  
  
## <a name="description"></a>说明  
 现有数据库维护计划已经过升级并可继续使用。 但是，您无法使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建新的数据库维护计划。 若要在对象资源管理器中查看维护计划，请展开“管理”，然后展开“早期”。 可以从任何数据库维护计划的上下文菜单中选择 "**迁移**"，将现有数据库维护计划迁移到新的格式。 由于新维护计划功能不能直接替代数据库维护计划，因此迁移后某些功能可能会丢失。 迁移数据库维护计划不会删除旧计划，因此可以在删除旧计划之前，先将其作为维护计划对其功能进行测试。  
  
 数据库维护计划中不再支持以下功能：  
  
-   日志传送  
  
-   "**数据库完整性检查**" 任务的 "**尝试修复任何次要问题**" 选项  
  
## <a name="corrective-action"></a>纠正措施  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 阻止日志传送包括在数据库维护计划中。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“日志传送”。  
  
  
