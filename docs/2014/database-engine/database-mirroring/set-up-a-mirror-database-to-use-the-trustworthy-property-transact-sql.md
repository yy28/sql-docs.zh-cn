---
title: 将镜像数据库设置为使用 Trustworthy 属性 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database option
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 6993b076-78ef-453e-b0ea-e341b8e5ee3e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 29cafc7e9669ca322571ff171961dd64cab114cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069507"
---
# <a name="set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql"></a>将镜像数据库设置为使用 Trustworthy 属性 (Transact-SQL)
  备份数据库时，TRUSTWORTHY 数据库属性设置为 OFF。 因此，在新的镜像数据库中，TRUSTWORTHY 始终为 OFF。 如果数据库在故障转移后需要得到信任，则必须在镜像开始后执行额外的设置步骤。  
  
> [!NOTE]  
>  有关此数据库属性的信息，请参阅 [TRUSTWORTHY 数据库属性](../../relational-databases/security/trustworthy-database-property.md)。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-setup-a-mirror-database-to-use-the-trustworthy-property"></a>将镜像数据库设置为使用 Trustworthy 属性  
  
1.  在主体服务器实例上，验证主体数据库是否已打开 Trustworthy 属性。  
  
    ```  
    SELECT name, database_id, is_trustworthy_on FROM sys.databases   
    ```  
  
     有关详细信息，请参阅 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)。  
  
2.  开始镜像后，验证数据库当前是否为主体数据库，会话是否正在使用同步运行模式以及是否已同步了会话。  
  
    ```  
    SELECT database_id, mirroring_role, mirroring_safety_level_desc, mirroring_state_desc FROM sys.database_mirroring  
    ```  
  
     有关详细信息，请参阅 [sys.database_mirroring (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql)。  
  
3.  一旦同步了镜像会话，就要手动故障转移到镜像数据库。  
  
     此操作既可以在 SQL Server Management Studio 中执行，也可以使用 Transact-SQL 执行：  
  
    -   [手动故障转移数据库镜像会话 (SQL Server Management Studio)](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [手动故障转移数据库镜像会话 (Transact-SQL)](manually-fail-over-a-database-mirroring-session-transact-sql.md)  
  
4.  使用以下 ALTER DATABASE 命令打开 Trustworthy 数据库属性：  
  
    ```  
    ALTER DATABASE <database_name> SET TRUSTWORTHY ON  
    ```  
  
     有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
5.  或者，再次手动故障转移，返回原始主体。  
  
6.  或者，通过将 SAFETY 设置为 OFF 并确保 WITNESS 也设置为 OFF，切换到异步、高性能模式。  
  
     在 Transact-SQL 中：  
  
    -   [更改数据库镜像会话中的事务安全 (Transact-SQL)](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
    -   [从数据库镜像会话删除见证服务器 (SQL Server)](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
     在 SQL Server Management Studio 中：  
  
    -   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="see-also"></a>请参阅  
 [TRUSTWORTHY 数据库属性](../../relational-databases/security/trustworthy-database-property.md)   
 [设置加密的镜像数据库](set-up-an-encrypted-mirror-database.md)  
  
  
