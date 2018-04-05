---
title: 主题服务器实例（配置数据库镜像安全向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47b9352af9dfa0c29a2536e82938663f6b56a36c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>主体服务器实例（配置数据库镜像安全向导）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用此页可以指定有关主体数据库的服务器实例的信息。 主体数据库是开始镜像会话的数据库的副本。 会话开始后，主体数据库是接受用户更改的数据库副本。 （当发生故障转移时，主体和镜像角色交换；因此，初始的主体数据库可能不再是主体数据库。）  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动配置数据库镜像安全向导 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>“常规”  
 **主体服务器实例**  
 因为 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的数据库镜像总是从主体服务器配置，所以当前的服务器实例总是为主体服务器实例。  
  
 **侦听器端口**  
 此选项的行为取决于此服务器实例是否存在镜像端点，如下所示：  
  
-   如果此服务器实例不存在侦听器端口，则端口号 5022 将显示在 **“端口”** 文本框中。 可以使用任何可用的端口号，例如 7022。  
  
-   如果镜像端点已经存在，则会显示该端点的端口号。 如果需要更改端口，请使用 ALTER ENDPOINT 命令。 有关详细信息，请参阅 [ALTER ENDPOINT (Transact-SQL)](../../t-sql/statements/alter-endpoint-transact-sql.md)。  
  
> [!NOTE]  
>  端口号是必需的。  
  
 **端点名称**  
 如果此服务器实例存在镜像端点，则端点名称将显示在此处。 如果端点不存在，则可以指定端点的名称。  
  
 **加密通过此端点发送的数据**  
 默认情况下，将启用加密。 如果启用，则要求（而不仅仅是支持）进行加密，并且所有加密选项都将使用默认值。 有关详细信息，请参阅 [CREATE ENDPOINT (Transact-SQL)](../../t-sql/statements/create-endpoint-transact-sql.md)的信息。  
  
 若要禁用加密，请清除此复选框。 若要重新启用加密，请选中此复选框。  
  
## <a name="see-also"></a>另请参阅  
 [数据库镜像终结点 (SQL Server)](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [数据库属性（“镜像”页）](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [启动数据库镜像监视器 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
