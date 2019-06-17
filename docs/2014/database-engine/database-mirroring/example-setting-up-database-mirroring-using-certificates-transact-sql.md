---
title: 例如：设置数据库镜像使用证书 (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: df489ecd-deee-465c-a26a-6d1bef6d7b66
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2eb63756a6ddf5e8a47f27f9f3d2f349c0bdf339
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806748"
---
# <a name="example-setting-up-database-mirroring-using-certificates-transact-sql"></a>例如：设置数据库镜像使用证书 (Transact SQL)
  此示例演示了使用基于证书的身份验证创建数据库镜像会话所需的所有阶段。 本主题中的示例使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 建议您对数据库镜像连接进行加密，除非您能够保证网络的安全。  
  
 将证书复制到其他系统时，请使用安全的复制方法。 必须格外小心地保证所有证书的安全。  
  
##  <a name="ExampleH2"></a> 示例  
 下面的示例演示必须对驻留在 HOST_A 上的一个伙伴执行哪些操作。 在此示例中，两个伙伴是三个计算机系统上的默认服务器实例。 两个服务器实例在非信任的 Windows 域中运行，因此需要基于证书的身份验证。  
  
 HOST_A 担当初始主体角色，HOST_B 担当镜像角色。  
  
 使用证书设置数据库镜像涉及四个常规阶段，本示例演示其中的三个阶段：1、2、4。 这些阶段如下：  
  
1.  [配置出站连接](#ConfiguringOutboundConnections)  
  
     本示例显示了下列操作的步骤：  
  
    1.  为出站连接配置 Host_A。  
  
    2.  为出站连接配置 Host_B。  
  
     有关设置数据库镜像的本阶段信息，请参阅 [允许数据库镜像终结点使用证书进行出站连接 (Transact-SQL)](database-mirroring-use-certificates-for-outbound-connections.md)。  
  
2.  [配置入站连接](#ConfigureInboundConnections)  
  
     本示例显示了下列操作的步骤：  
  
    1.  为入站连接配置 Host_A。  
  
    2.  为入站连接配置 Host_B。  
  
     有关设置数据库镜像的本阶段信息，请参阅 [允许数据库镜像终结点将证书用于入站连接 (Transact-SQL)](database-mirroring-use-certificates-for-inbound-connections.md)。  
  
3.  创建镜像数据库  
  
     有关如何创建镜像数据库的信息，请参阅 [为镜像准备镜像数据库 (SQL Server)](prepare-a-mirror-database-for-mirroring-sql-server.md)。  
  
4.  [配置镜像伙伴](#ConfigureMirroringPartners)  
  
###  <a name="ConfiguringOutboundConnections"></a> 配置出站连接  
 **为出站连接配置 Host_A**  
  
1.  在 master 数据库中，创建数据库主密钥（如果需要）。  
  
    ```  
    USE master;  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<1_Strong_Password!>';  
    GO  
    ```  
  
2.  为此服务器实例制作一个证书。  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_A_cert   
       WITH SUBJECT = 'HOST_A certificate';  
    GO  
    ```  
  
3.  使用该证书为服务器实例创建一个镜像端点。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_A_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
4.  备份 HOST_A 证书，并将其复制到其他系统，即 HOST_B。  
  
    ```  
    BACKUP CERTIFICATE HOST_A_cert TO FILE = 'C:\HOST_A_cert.cer';  
    GO  
    ```  
  
5.  使用任一安全的复制方法，将 C:\HOST_A_cert.cer 复制到 HOST_B。  
  
 **为出站连接配置 Host_B**  
  
1.  在 master 数据库中，创建数据库主密钥（如果需要）。  
  
    ```  
    USE master;  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Strong_Password_#2>';  
    GO  
    ```  
  
2.  为 HOST_B 服务器实例制作一个证书。  
  
    ```  
    CREATE CERTIFICATE HOST_B_cert   
       WITH SUBJECT = 'HOST_B certificate for database mirroring';  
    GO  
    ```  
  
3.  在 HOST_B 中为服务器实例创建一个镜像端点。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_B_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
4.  备份 HOST_B 证书。  
  
    ```  
    BACKUP CERTIFICATE HOST_B_cert TO FILE = 'C:\HOST_B_cert.cer';  
    GO   
    ```  
  
5.  使用任一安全的复制方法，将 C:\HOST_B_cert.cer 复制到 HOST_A。  
  
 有关详细信息，请参阅 [允许数据库镜像终结点使用证书进行出站连接 (Transact-SQL)](database-mirroring-use-certificates-for-outbound-connections.md)。  
  
###  <a name="ConfigureInboundConnections"></a> 配置入站连接  
 **为入站连接配置 Host_A**  
  
1.  在 HOST_A 上为 HOST_B 创建一个登录名。  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
2.  创建一个使用该登录名的用户。  
  
    ```  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
3.  使证书与该用户关联。  
  
    ```  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
4.  授予对远程镜像端点的登录名的 CONNECT 权限。  
  
    ```  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
 **为入站连接配置 Host_B**  
  
1.  在 HOST_B 上为 HOST_A 创建一个登录名。  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_A_login WITH PASSWORD = '=Sample#2_Strong_Password2';  
    GO  
    ```  
  
2.  创建一个使用该登录名的用户。  
  
    ```  
    CREATE USER HOST_A_user FOR LOGIN HOST_A_login;  
    GO  
    ```  
  
3.  使证书与该用户关联。  
  
    ```  
    CREATE CERTIFICATE HOST_A_cert  
       AUTHORIZATION HOST_A_user  
       FROM FILE = 'C:\HOST_A_cert.cer'  
    GO  
    ```  
  
4.  授予对远程镜像端点的登录名的 CONNECT 权限。  
  
    ```  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_A_login];  
    GO  
    ```  
  
> [!IMPORTANT]  
>  如果打算在具有自动故障转移功能的高安全性模式下运行，则必须重复相同的设置步骤为出站连接和入站连接配置见证服务器。 设置入站连接时，如果涉及到见证服务器，则需要为两个伙伴的见证服务器和见证服务器的两个伙伴设置登录名和用户。  
  
 有关详细信息，请参阅 [允许数据库镜像终结点将证书用于入站连接 (Transact-SQL)](database-mirroring-use-certificates-for-inbound-connections.md)。  
  
### <a name="creating-the-mirror-database"></a>创建镜像数据库  
 有关如何创建镜像数据库的信息，请参阅 [为镜像准备镜像数据库 (SQL Server)](prepare-a-mirror-database-for-mirroring-sql-server.md)。  
  
###  <a name="ConfigureMirroringPartners"></a> 配置镜像伙伴  
  
1.  在 HOST_B 的镜像服务器实例上，将 HOST_A 上的服务器实例设置为伙伴（使其成为初始主体服务器实例）。 将 `TCP://HOST_A.Mydomain.Corp.Adventure-Works``.com:7024`替换为有效的网络地址。 有关详细信息，请参阅 [指定服务器网络地址（数据库镜像）](specify-a-server-network-address-database-mirroring.md)。  
  
    ```  
    --At HOST_B, set server instance on HOST_A as partner (principal server):  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://HOST_A.Mydomain.Corp.Adventure-Works.com:7024';  
    GO  
    ```  
  
2.  在 HOST_A 的主体服务器实例上，将 HOST_B 上的服务器实例设置为伙伴（使其成为初始镜像服务器实例）。 将 `TCP://HOST_B.Mydomain.Corp.Adventure-Works.com:7024`替换为有效的网络地址。  
  
    ```  
    --At HOST_A, set server instance on HOST_B as partner (mirror server).  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://HOST_B.Mydomain.Corp.Adventure-Works.com:7024';  
    GO  
    ```  
  
3.  此示例假设会话将在高性能模式下运行。 若要在高性能模式下配置此会话，在主体服务器实例上（位于 HOST_A 上），将事务安全性设置为 OFF。  
  
    ```  
    --Change to high-performance mode by turning off transacton safety.  
    ALTER DATABASE AdventureWorks   
        SET PARTNER SAFETY OFF  
    GO  
    ```  
  
    > [!NOTE]  
    >  如果你想要在具有自动故障转移功能的高安全性模式下运行，将事务安全性设置为 FULL （默认设置） 和执行第二个 SET PARTNER 后尽快添加见证服务器 **' *`partner_server`* '** 语句。 注意，必须首先为出站连接和入站连接配置见证服务器。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [为镜像准备镜像数据库 (SQL Server)](prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [允许数据库镜像终结点将证书用于入站连接 (Transact-SQL)](database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [允许数据库镜像终结点使用证书进行出站连接 (Transact-SQL)](database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [角色切换后登录名和作业的管理 (SQL Server)](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
-   [当数据库在其他服务器实例上可用时管理元数据 (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md) (SQL Server)  
  
-   [数据库镜像配置故障排除 (SQL Server)](troubleshoot-database-mirroring-configuration-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [传输安全模式的数据库镜像和 AlwaysOn 可用性组&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [指定服务器网络地址（数据库镜像）](specify-a-server-network-address-database-mirroring.md)   
 [数据库镜像终结点 (SQL Server)](the-database-mirroring-endpoint-sql-server.md)   
 [使用数据库镜像终结点证书 (Transact-SQL)](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [SQL Server 数据库引擎和 Azure SQL Database 的安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
