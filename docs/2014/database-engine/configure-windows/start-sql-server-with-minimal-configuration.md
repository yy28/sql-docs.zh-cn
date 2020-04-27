---
title: 以最小配置启动 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cf7065d064e322e45fb95a38aed514b2acfc714a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62756223"
---
# <a name="start-sql-server-with-minimal-configuration"></a>以最小配置启动 SQL Server
  如果存在配置问题而无法启动服务器，可使用最小配置启动选项来启动 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 这就是启动选项 **-f**。 使用最小配置启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例会自动将服务器置于单用户模式。  
  
 在最小配置模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，注意下列事项：  
  
-   只有一个用户可以连接到服务器，并且不会执行 CHECKPOINT 进程。  
  
-   远程访问和预读功能将被禁用。  
  
-   启动存储过程将不运行。  
  
 用最小配置启动服务器后，应更改相应的服务器选项值，然后停止并重新启动服务器。  
  
> [!IMPORTANT]  
>  使用 **sqlcmd** 实用工具和专用管理员连接 (DAC) 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果使用典型连接，则在最小配置模式下连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之前，停止 SQL Server 代理服务。 否则，SQL Server 代理服务将使用该连接从而使其阻塞。  
  
## <a name="see-also"></a>另请参阅  
 [启动、停止或暂停 SQL Server 代理服务](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)   
 [用于数据库管理员的诊断连接](diagnostic-connection-for-database-administrators.md)   
 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [数据库引擎服务启动选项](database-engine-service-startup-options.md)  
  
  
