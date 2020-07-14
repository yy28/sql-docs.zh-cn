---
title: affinity64 mask 服务器配置选项 | Microsoft Docs
description: 了解 affinity64 mask 选项。 了解何时在 SQL Server 中使用它将处理器绑定到特定线程。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- affinity64 mask option
- binding processors [SQL Server]
ms.assetid: 75ed08c7-f85c-4e15-9ee1-e7bc545d3293
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 452075955c30d7e49eb317f40bf377a6e894af29
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85631411"
---
# <a name="affinity64-mask-server-configuration-option"></a>affinity64 mask 服务器配置选项
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  affinity64 mask 将处理器绑定到特定的线程，这与 affinity mask 选项相似。 使用 affinity mask 可以绑定前 32 个处理器，而使用 affinity64 mask 可以绑定计算机上余下的处理器。 此选项仅出现在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 64 位版本中。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] 改为使用 [ALTER SERVER CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-server-configuration-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [affinity mask 服务器配置选项](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
