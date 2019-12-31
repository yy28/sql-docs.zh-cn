---
title: 创建可用性组 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: 8b0a6301-8b79-4415-b608-b40876f30066
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7b09bb2f08095af33f80fe4161032036482f835
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228793"
---
# <a name="create-an-availability-group-transact-sql"></a>创建可用性组 (Transact-SQL)
  本主题介绍如何使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 在启用了 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 功能的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 实例上创建和配置可用性组。 “可用性组” ** 定义一组用户数据库，这些用户数据库将以支持故障转移的单个单元和一组故障转移伙伴（称作“可用性副本” **）的形式进行故障转移。  
  
> [!NOTE]  
>  有关可用性组的简介，请参阅 [AlwaysOn 可用性组概述 (SQL Server)](overview-of-always-on-availability-groups-sql-server.md)。  

> [!NOTE]  
>  除了使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]之外，您还可以使用“创建可用性组”向导或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell cmdlet。 有关详细信息，请参阅 [使用可用性组向导 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)、 [使用“新建可用性组”对话框 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)或 [创建可用性组 (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)。  
  
##  <a name="BeforeYouBegin"></a>开始之前  
 我们强烈建议您首先阅读此部分，再尝试创建您的第一个可用性组。  
  
###  <a name="PrerequisitesRestrictions"></a>先决条件、限制和建议  
  
-   创建可用性组之前，请先验证承载可用性副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例位于同一 WSFC 故障转移群集内的不同 Windows Server 故障转移群集 (WSFC) 节点上。 此外，还请验证每个服务器实例是否都满足所有其他 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 先决条件。 有关详细信息，我们强烈建议你参阅[针对 AlwaysOn 可用性组的先决条件、限制和建议 (SQL Server)](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
###  <a name="Security"></a>安全  
  
####  <a name="Permissions"></a>访问  
 需要 **sysadmin** 固定服务器角色的成员资格，以及 CREATE AVAILABILITY GROUP 服务器权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
###  <a name="SummaryTsqlStatements"></a>任务和相应 Transact-sql 语句摘要  
 下表列出了涉及创建和配置可用性组的基本任务，并且指出了要用于这些任务的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句。 必须按照任务在表中出现的顺序执行 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 任务。  
  
|任务|Transact-SQL 语句|执行任务的位置**<sup>*</sup>**|  
|----------|----------------------------------|-------------------------------------------|  
|创建数据库镜像端点（每个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例一次）|[创建终结点终结点](/sql/t-sql/statements/create-endpoint-transact-sql) *...* 对于 DATABASE_MIRRORING|在缺少数据库镜像端点的每个服务器实例上执行。|  
|创建可用性组|[创建可用性组](/sql/t-sql/statements/create-availability-group-transact-sql)|在要承载初始主副本的服务器实例上执行。|  
|将辅助副本联接到可用性组|[更改可用性组](join-a-secondary-replica-to-an-availability-group-sql-server.md) *group_name*联接|在承载辅助副本的各服务器实例上执行。|  
|准备辅助数据库|[备份](/sql/t-sql/statements/backup-transact-sql)和[还原](/sql/t-sql/statements/restore-statements-transact-sql)。|在承载主副本的服务器实例上创建备份。<br /><br /> 使用 RESTORE WITH NORECOVERY 在承载辅助副本的各服务器实例上还原备份。|  
|通过将各辅助数据库联接到可用性组，开始数据同步|[更改数据库](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) *DATABASE_NAME*设置 HADR 可用性组 = *group_name*|在承载辅助副本的各服务器实例上执行。|  
  
 **<sup>*</sup>** 若要执行给定任务，请连接到指示的服务器实例。  
  
##  <a name="TsqlProcedure"></a>使用 Transact-sql 创建和配置可用性组  
  
> [!NOTE]  
>  有关包含上述各 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句的代码示例的配置过程示例，请参阅 [示例：配置使用 Windows 身份验证的可用性组](#ExampleConfigAGWinAuth)。  
  
1.  连接到要承载主副本的服务器实例。  
  
2.  使用[create availability group](/sql/t-sql/statements/create-availability-group-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)]语句创建可用性组。  
  
3.  将新的辅助副本联接到可用性组。 有关详细信息，请参阅 [将辅助副本联接到可用性组 (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)。  
  
4.  对于可用性组中的每个数据库，通过使用 RESTORE WITH NORECOVERY 还原主数据库的最近的备份，创建辅助数据库。 有关详细信息，请参阅 [示例：使用 Windows 身份验证设置可用性组 (Transact-SQL)](create-an-availability-group-transact-sql.md)，从还原数据库备份的步骤开始。  
  
5.  将每个新的辅助数据库联接到可用性组。 有关详细信息，请参阅 [将辅助副本联接到可用性组 (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)。  
  
##  <a name="ExampleConfigAGWinAuth"></a>示例：配置使用 Windows 身份验证的可用性组  
 此示例创建一个示例 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 配置过程，该过程使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 设置使用 Windows 身份验证的数据库镜像端点并且创建和配置一个可用性组及其辅助数据库。  
  
 此示例包含以下部分：  
  
-   [使用示例配置过程的先决条件](#PrerequisitesForExample)  
  
-   [示例配置过程](#SampleProcedure)  
  
-   [示例配置过程的完整代码示例](#CompleteCodeExample)  
  
###  <a name="PrerequisitesForExample"></a>使用示例配置过程的先决条件  
 此示例过程具有以下要求：  
  
-   服务器实例必须支持 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 有关详细信息，请参阅[AlwaysOn 可用性组 &#40;SQL Server&#41;的先决条件、限制和建议](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
-   两个示例数据库 *MyDb1* 和 *MyDb2*必须在将承载主副本的服务器实例上存在。 下面的代码示例创建和配置这两个数据库，并且创建这两个数据库的完整备份。 在您想要创建示例可用性组的服务器实例上执行这些代码示例。 此服务器实例将承载示例可用性组的初始主副本。  
  
    1.  下面的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 示例创建这些数据库并且将它们更改为使用完整恢复模式：  
  
        ```sql
        -- Create sample databases:  
        CREATE DATABASE MyDb1;  
        GO  
        ALTER DATABASE MyDb1 SET RECOVERY FULL;  
        GO  
  
        CREATE DATABASE MyDb2;  
        GO  
        ALTER DATABASE MyDb2 SET RECOVERY FULL;  
        GO  
        ```  
  
    2.  下面的代码示例创建 *MyDb1* 和 *MyDb2*的完整数据库备份。 此\\ \\代码示例使用*虚构的备份*\\共享*SQLbackups*。  
  
        ```sql
        -- Backup sample databases:  
        BACKUP DATABASE MyDb1   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
            WITH FORMAT  
        GO  
  
        BACKUP DATABASE MyDb2   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
            WITH FORMAT  
        GO
        ```  
  
###  <a name="SampleProcedure"></a>示例配置过程  
 在这个示例配置中，将在两个独立服务器实例上创建可用性副本，这些服务器实例的服务帐户在不同的可信域（`DOMAIN1` 和 `DOMAIN2`）下运行。  
  
 下表总结了此示例配置中使用的值。  
  
|初始角色|System|主机 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例|  
|------------------|------------|---------------------------------------------|  
|主要|`COMPUTER01`|`AgHostInstance`|  
|辅助|`COMPUTER02`|默认实例。|  
  
1.  在你计划创建可用性组的服务器实例（这是 *上名为* 的实例）上创建名为 `AgHostInstance` dbm_endpoint `COMPUTER01`的数据库镜像端点。 此端点使用端口 7022。 请注意，您要在其上创建可用性组的服务器实例将承载主副本。  
  
    ```sql
    -- Create endpoint on server instance that hosts the primary replica:  
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO
    ```  
  
2.  在将承载辅助副本的服务器实例（这是 *上的默认服务器实例）上创建端点* dbm_endpoint `COMPUTER02`。 此端点使用端口 5022。  
  
    ```sql
    -- Create endpoint on server instance that hosts the secondary replica:   
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=5022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO
    ```  
  
3.  > [!NOTE]  
    >  如果要承载您的可用性副本的服务器实例的服务帐户基于相同的域帐户运行，则不需要执行此步骤。 跳过它，直接进入下一步。  
  
     如果该服务器实例的服务帐户基于不同的域用户运行，则在各服务器实例上，为其他服务器实例创建一个登录名，并且授予此登录名访问本地数据库镜像端点的权限。  
  
     下面的代码示例说明用于创建一个登录名并且向该登录名授予针对某一端点的权限的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句。 远程服务器实例的域帐户在此处表示为*domain_name*\\*user_name*。  
  
    ```sql
    -- If necessary, create a login for the service account, domain_name\user_name  
    -- of the server instance that will host the other replica:  
    USE master;  
    GO  
    CREATE LOGIN [domain_name\user_name] FROM WINDOWS;  
    GO  
    -- And Grant this login connect permissions on the endpoint:  
    GRANT CONNECT ON ENDPOINT::dbm_endpoint   
       TO [domain_name\user_name];  
    GO  
    ```  
  
4.  在用户数据库驻留的服务器实例上，创建可用性组。  
  
     下面的代码示例在创建了示例数据库 *MyDb1* 和 *MyDb2* 的服务器实例上创建名为 *MyAG*的可用性组。 首先指定 `AgHostInstance`COMPUTER01 *上的本地服务器实例* 。 该实例将承载初始的主副本。 指定远程服务器实例（ *COMPUTER02*上的默认服务器实例）承载辅助副本。 将两个可用性副本配置为使用异步提交模式和手动故障转移（对于异步提交副本，手动故障转移意味着强制故障转移可能造成数据丢失）。  
  
    ```sql
    -- Create the availability group, MyAG:   
    CREATE AVAILABILITY GROUP MyAG   
       FOR   
          DATABASE MyDB1, MyDB2   
       REPLICA ON   
          'COMPUTER01\AgHostInstance' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',   
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             ),  
          'COMPUTER02' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );   
    GO  
    ```  
  
     有关创建可用性组的其他 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 代码示例，请参阅 [CREATE AVAILABILITY GROUP (Transact-SQL);](/sql/t-sql/statements/create-availability-group-transact-sql)  
  
5.  在承载辅助副本的服务器实例上，将辅助副本联接到可用性组。  
  
     下面的代码示例将 `COMPUTER02` 上的辅助副本联接到 `MyAG` 可用性组。  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- join the secondary replica to the availability group:  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    GO  
    ```  
  
6.  在承载辅助副本的服务器实例上，创建辅助数据库。  
  
     以下代码示例通过使用 RESTORE WITH NORECOVERY 还原数据库备份来创建 *MyDb1* 和 *MyDb2* 辅助数据库。  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- Restore database backups using the WITH NORECOVERY option:  
    RESTORE DATABASE MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NORECOVERY  
    GO  
  
    RESTORE DATABASE MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH NORECOVERY  
    GO
    ```  
  
7.  在承载主副本的服务器实例上，备份每个主数据库上的事务日志。  
  
    > [!IMPORTANT]  
    >  在您配置真实的可用性组时，我们建议在进行此日志备份之前，挂起针对您的主数据库的日志备份任务，直到您将相应的辅助数据库联接到该可用性组。  
  
     下面的代码示例在 MyDb1 和 MyDb2 上创建一个事务日志备份。  
  
    ```sql
    -- On the server instance that hosts the primary replica,   
    -- Backup the transaction log on each primary database:  
    BACKUP LOG MyDb1   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NOFORMAT  
    GO  
  
    BACKUP LOG MyDb2   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITHNOFORMAT  
    GO
    ```  
  
    > [!TIP]  
    >  通常，日志备份必须在每个主数据库上进行，然后在相应的辅助数据库上还原（使用 WITH NORECOVERY）。 但是，如果数据库刚刚创建而尚未进行日志备份，或者如果恢复模式刚刚从 SIMPLE 更改为 FULL，则不必进行此日志备份。  
  
8.  在承载辅助副本的服务器实例上，将日志备份应用于辅助数据库。  
  
     以下代码示例通过使用 RESTORE WITH NORECOVERY 还原数据库备份来将备份应用于 *MyDb1* 和 *MyDb2* 辅助数据库。  
  
    > [!IMPORTANT]  
    >  在您准备真实的辅助数据库时，需要应用您从其创建了辅助数据库的数据库备份之后发生的每个日志备份，从最早的开始并且始终使用 RESTORE WITH NORECOVERY。 当然，如果您还原完整和差异数据库备份，则只需应用在差异备份后发生的日志备份。  
  
    ```sql
    -- Restore the transaction log on each secondary database,  
    -- using the WITH NORECOVERY option:  
    RESTORE LOG MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    RESTORE LOG MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
9. 在承载辅助副本的服务器实例上，将新的辅助数据库联接到可用性组。  
  
     下面的代码示例依次将 *MyDb1* 辅助数据库和 *MyDb2* 辅助数据库联接到 *MyAG* 可用性组。  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- join each secondary database to the availability group:  
    ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
    GO  
  
    ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
    GO
    ```  
  
###  <a name="CompleteCodeExample"></a>示例配置过程的完整代码示例  
 下面的示例合并了示例配置过程的所有步骤中的代码示例。 下表总结了此代码示例中使用的占位符值。 有关此代码示例中的步骤的详细信息，请参阅本主题中前面的 [使用示例配置过程的先决条件](#PrerequisitesForExample) 和 [示例配置过程](#SampleProcedure)。  
  
|占位符|说明|  
|-----------------|-----------------|  
|\\\\**\\*SQLbackups*|虚构的备份共享。|  
|\\\\**\\*SQLbackups\MyDb1.bak*|MyDb1 的备份文件。|  
|\\\\**\\*SQLbackups\MyDb2.bak*|MyDb2 的备份文件。|  
|*7022*|分配给各数据库镜像端点的端口号。|  
|*COMPUTER01\AgHostInstance*|承载初始主副本的服务器实例。|  
|*COMPUTER02*|承载初始辅助副本的服务器实例。 这是 `COMPUTER02`上的默认服务器实例。|  
|*dbm_endpoint*|为每个数据库镜像端点指定的名称。|  
|*MyAG*|示例可用性组的名称。|  
|*MyDb1*|第一个示例数据库的名称。|  
|*MyDb2*|第二个示例数据库的名称。|  
|*DOMAIN1\user1*|要承载初始主副本的服务器实例的服务帐户。|  
|*DOMAIN2\user2*|要承载初始辅助副本的服务器实例的服务帐户。|  
|TCP://*COMPUTER01.Adventure-Works.com*:*7022*|COMPUTER01 上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 AgHostInstance 实例的端点 URL。|  
|TCP://*COMPUTER02.Adventure-Works.com*:*5022*|COMPUTER02 上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的默认实例的端点 URL。|  
  
> [!NOTE]  
>  有关创建可用性组的其他 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 代码示例，请参阅 [CREATE AVAILABILITY GROUP (Transact-SQL);](/sql/t-sql/statements/create-availability-group-transact-sql)  
  
```sql
-- on the server instance that will host the primary replica,   
-- create sample databases:  
CREATE DATABASE MyDb1;  
GO  
ALTER DATABASE MyDb1 SET RECOVERY FULL;  
GO  
  
CREATE DATABASE MyDb2;  
GO  
ALTER DATABASE MyDb2 SET RECOVERY FULL;  
GO  
  
-- Backup sample databases:  
BACKUP DATABASE MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FORMAT  
GO  
  
BACKUP DATABASE MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FORMAT  
GO  
  
-- Create the endpoint on the server instance that will host the primary replica:  
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- Create the endpoint on the server instance that will host the secondary replica:   
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the primary replica,   
-- create a login for the service account   
-- of the server instance that will host the secondary replica, DOMAIN2\user2,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
CREATE LOGIN [DOMAIN2\user2] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN2\user2];  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the secondary replica,  
-- create a login for the service account   
-- of the server instance that will host the primary replica, DOMAIN1\user1,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
  
CREATE LOGIN [DOMAIN1\user1] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN1\user1];  
GO  
  
-- On the server instance that will host the primary replica,   
-- create the availability group, MyAG:  
CREATE AVAILABILITY GROUP MyAG   
   FOR   
      DATABASE MyDB1, MyDB2   
   REPLICA ON   
      'COMPUTER01\AgHostInstance' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         ),  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         );   
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join the secondary replica to the availability group:  
ALTER AVAILABILITY GROUP MyAG JOIN;  
GO  
  
-- Restore database backups onto this server instance, using RESTORE WITH NORECOVERY:  
RESTORE DATABASE MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NORECOVERY  
GO  
  
RESTORE DATABASE MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH NORECOVERY  
GO  
  
-- Back up the transaction log on each primary database:  
BACKUP LOG MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NOFORMAT  
GO  
  
BACKUP LOG MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITHNOFORMAT  
GO  
  
-- Restore the transaction log on each secondary database,  
-- using the WITH NORECOVERY option:  
RESTORE LOG MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FILE=1, NORECOVERY  
GO  
RESTORE LOG MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FILE=1, NORECOVERY  
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join each secondary database to the availability group:  
ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
GO  
  
ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
GO
```  
  
##  <a name="RelatedTasks"></a>相关任务  
 **配置可用性组和副本属性**  
  
-   [更改可用性副本的可用性模式 &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [更改可用性副本的故障转移模式 &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [创建或配置可用性组侦听器 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [配置灵活的故障转移策略以控制自动故障转移的条件（AlwaysOn 可用性组）](configure-flexible-automatic-failover-policy.md)  
  
-   [在添加或修改可用性副本时指定终结点 URL &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [在可用性副本上配置备份 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [配置对可用性副本的只读访问 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [为可用性组 &#40;SQL Server 配置只读路由&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [更改可用性副本的会话超时期限 &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **完成可用性组配置**  
  
-   [将辅助副本联接到可用性组 &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [为可用性组手动准备辅助数据库 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [将辅助数据库联接到可用性组 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [创建或配置可用性组侦听器 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **创建可用性组的替代方法**  
  
-   [使用可用性组向导 &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用 "新建可用性组" 对话框 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [创建可用性组 &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
 **启用 AlwaysOn 可用性组**  
  
-   [启用和禁用 AlwaysOn 可用性组 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **配置数据库镜像端点**  
  
-   [为 AlwaysOn 可用性组 &#40;SQL Server PowerShell 创建数据库镜像端点&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [为 Windows 身份验证创建数据库镜像端点 &#40;Transact-sql&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [将证书用于数据库镜像端点 &#40;Transact-sql&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [在添加或修改可用性副本时指定终结点 URL &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **解决 AlwaysOn 可用性组配置问题**  
  
-   [删除 AlwaysOn 可用性组配置（SQL Server）的故障排除](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [排除失败的添加文件操作 &#40;AlwaysOn 可用性组&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a>相关内容  
  
-   **博客**  
  
     [AlwaysON - HADRON 学习系列：启用了 HADRON 的数据库的工作线程池用法](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn 团队博客：SQL Server AlwaysOn 团队官方博客](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程师博客](https://blogs.msdn.com/b/psssql/)  
  
-   **视频**  
  
     [Microsoft SQL Server Code-Named "Denali" AlwaysOn 系列，第一部分：介绍下一代高可用性解决方案](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named "Denali" AlwaysOn 系列，第二部分：使用 AlwaysOn 生成关键任务高可用性解决方案](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **白皮书**  
  
     [用于高可用性和灾难恢复的 Microsoft SQL Server AlwaysOn 解决方案指南](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 的 Microsoft 白皮书](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客户咨询团队白皮书](http://sqlcat.com/)  
  
## <a name="see-also"></a>另请参阅  
 [数据库镜像端点 &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性组侦听器、客户端连接和应用程序故障转移 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
