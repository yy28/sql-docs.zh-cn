---
title: affinity64 I/O mask 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7449be34c7697f770b18357c465da41cd57164b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210157"
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>affinity64 I/O mask 服务器配置选项
  **affinity64 I/O mask** 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] affinity I/O mask **选项类似，用于将** 磁盘 I/O 绑定到指定的 CPU 子集。 使用 **affinity I/O mask** 只能绑定前 32 个处理器，而使用 **affinity64 I/O mask** 可以绑定计算机上剩余的处理器。 如果重新配置 **affinity64 I/O mask**，则必须重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 此选项仅出现在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 64 位版本中。  
  
## <a name="see-also"></a>请参阅  
 [affinity I/O mask 服务器配置选项](affinity-input-output-mask-server-configuration-option.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
