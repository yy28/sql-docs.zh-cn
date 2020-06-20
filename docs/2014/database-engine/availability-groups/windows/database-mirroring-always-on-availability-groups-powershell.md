---
title: 为 AlwaysOn 可用性组创建数据库镜像端点（SQL Server PowerShell） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], endpoint
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 56058ff8aa72d2471381dd87fb25a3b68356ed36
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936878"
---
# <a name="create-a-database-mirroring-endpoint-for-alwayson-availability-groups-sql-server-powershell"></a>为 AlwaysOn 可用性组创建数据库镜像端点 (SQL Server PowerShell)
  本主题介绍如何使用 PowerShell 创建供 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 使用的数据库镜像端点。  
  
 **本主题内容**  
  
-   **开始之前：**  [安全性](#Security)  
  
-   **若要创建数据库镜像端点，请使用：**  [PowerShell](#PowerShellProcedure)  
  
## <a name="before-you-begin"></a>开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
> [!IMPORTANT]  
>  不推荐使用 RC4 算法。 [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] 我们建议使用 AES。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 要求具有 CREATE ENDPOINT 权限，或者具有 sysadmin 固定服务器角色的成员身份。 有关详细信息，请参阅 [GRANT 终结点权限 (Transact-SQL)](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)。  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  
 **创建数据库镜像端点**  
  
1.  将目录 (`cd`) 更改到要为其创建数据库镜像端点的服务器实例。  
  
2.  使用 `New-SqlHadrEndpoint` cmdlet 创建端点，然后使用 `Set-SqlHadrEndpoint` 启动此端点。  
  
###  <a name="example-powershell"></a><a name="PShellExample"></a> 示例 (PowerShell)  
 以下 PowerShell 命令在 SQL Server （*计算机* \\ *实例*）的实例上创建数据库镜像端点。 该端点使用端口 5022。  
  
> [!IMPORTANT]  
>  此示例只适用于目前缺少数据库镜像端点的服务器实例。  
  
```powershell
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
 **配置数据库镜像端点**  
  
-   [为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [使用数据库镜像终结点证书 (Transact-SQL)](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [允许数据库镜像终结点使用证书进行出站连接 (Transact-SQL)](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [允许数据库镜像终结点将证书用于入站连接 (Transact-SQL)](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [指定服务器网络地址（数据库镜像）](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [在添加或修改可用性副本时指定终结点 URL (SQL Server)](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **查看有关数据库镜像端点的信息**  
  
-   [sys.database_mirroring_endpoints (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql 创建可用性组&#41;](create-an-availability-group-transact-sql.md)   
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)  
