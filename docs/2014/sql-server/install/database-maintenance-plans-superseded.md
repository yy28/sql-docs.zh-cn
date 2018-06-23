---
title: 数据库维护计划取代 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- suspended database maintenance plans
- database maintenance plans [SQL Server Agent]
- maintenance plans [SQL Server Agent]
ms.assetid: efac127c-6c81-4c7a-a6c4-9aae5d15545d
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f71e0cb8cb94cba893403f31cb2ffb9ee229c4ca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024265"
---
# <a name="database-maintenance-plans-superseded"></a>数据库维护计划被取代
    
## <a name="component"></a>组件  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>Description  
 现有数据库维护计划已经过升级并可继续使用。 但是，您无法使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建新的数据库维护计划。 若要在对象资源管理器中查看维护计划，请展开“管理”，然后展开“早期”。 你可以通过选择现有的数据库维护计划迁移到新格式**迁移**从任何数据库维护计划的上下文菜单。 由于新维护计划功能不能直接替代数据库维护计划，因此迁移后某些功能可能会丢失。 迁移数据库维护计划不会删除旧计划，因此可以在删除旧计划之前，先将其作为维护计划对其功能进行测试。  
  
 数据库维护计划中不再支持以下功能：  
  
-   日志传送  
  
-   **尝试解决所有次要问题**选项**数据库完整性检查**任务  
  
## <a name="corrective-action"></a>纠正措施  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 阻止日志传送包括在数据库维护计划中。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“日志传送”。  
  
  