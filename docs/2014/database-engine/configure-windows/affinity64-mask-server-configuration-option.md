---
title: affinity64 mask 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- affinity64 mask option
- binding processors [SQL Server]
ms.assetid: 75ed08c7-f85c-4e15-9ee1-e7bc545d3293
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ee993d620614b0cb7bbf09c77209a2413104fb9c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48071377"
---
# <a name="affinity64-mask-server-configuration-option"></a>affinity64 mask 服务器配置选项
  affinity64 mask 将处理器绑定到特定的线程，这与 affinity mask 选项相似。 使用 affinity mask 可以绑定前 32 个处理器，而使用 affinity64 mask 可以绑定计算机上余下的处理器。 此选项仅出现在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 64 位版本中。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] 改为使用 [ALTER SERVER CONFIGURATION (Transact-SQL)](/sql/t-sql/statements/alter-server-configuration-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [affinity mask 服务器配置选项](affinity-mask-server-configuration-option.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
