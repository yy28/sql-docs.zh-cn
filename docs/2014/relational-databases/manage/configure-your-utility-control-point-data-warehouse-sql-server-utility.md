---
title: 配置实用工具控制点数据仓库（SQL Server 实用工具）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2f18f10d58bb9b5d83c2b23046c68c886a91084c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137525"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>配置您的实用工具控制点数据仓库（SQL Server 实用工具）
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例收集的数据存储在实用工具管理数据仓库 (UMDW) 中；UMDW 文件名为 sysutility_mdw。  
  
 您可以配置 UMDW 数据保持期。 有关详细信息，请参阅[实用工具管理（SQL Server 实用工具）](../../database-engine/utility-administration-sql-server-utility.md)。  
  
 以下配置设置在此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不可配置：  
  
-   UMDW 名称：Sysutility_mdw。  
  
-   收集组上载频率：每隔 15 分钟。  
  
 UMDW 目录是可配置的：\<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\，其中，\<System drive> 通常为 C:\ 驱动器。 日志文件 Sysutility_mdw_\<GUID>_LOG 位于同一目录中。  
  
> [!NOTE]  
>  可以使用 detach/attach 或 ALTER DATABASE 更改该 UMDW (sysutility_mdw) 文件位置。 我们建议使用 ALTER DATABASE。 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 实用工具功能和任务](sql-server-utility-features-and-tasks.md)  
  
  
