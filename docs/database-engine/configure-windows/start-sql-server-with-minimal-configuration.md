---
title: 以最小配置启动 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0c919ad9202c99c7b010b6aee9c921e76784eb24
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "79027956"
---
# <a name="start-sql-server-with-minimal-configuration"></a>以最小配置启动 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  如果存在配置问题而无法启动服务器，可使用最小配置启动选项来启动 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 这就是启动选项 **-f**。 使用最小配置启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例会自动将服务器置于单用户模式。  
  
 在最小配置模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，注意下列事项：  
  
-   只有一个用户可以连接，并且不会执行 `CHECKPOINT` 进程。  
  
-   远程访问和预读功能将被禁用。  
  
-   启动存储过程将不运行。  

-   将以最小大小配置 `tempdb`。

-   审核将处于禁用状态，但仍可发出审核 DDL。 实际上，-m 应该足以满足大多数需要 SQL Server 审核重新配置的情况  。 有关审核配置中的安全性的更多详细信息，请参阅 [SQL Server 中的审核](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/dd392015(v=sql.100)#security)。
  
 用最小配置启动服务器后，应更改相应的服务器选项值，然后停止并重新启动服务器。  
  
> [!IMPORTANT]  
>  使用 **sqlcmd** 实用工具和专用管理员连接 (DAC) 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果使用典型连接，则在最小配置模式下连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之前，停止 SQL Server 代理服务。 否则，SQL Server 代理服务将使用该连接从而使其阻塞。  
  
## <a name="see-also"></a>另请参阅  
 [启动、停止或暂停 SQL Server 代理服务](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [用于数据库管理员的诊断连接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [数据库引擎服务启动选项](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
