---
title: 使用分离和附加升级数据库 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- upgrading databases
- database upgrades [SQL Server]
- database detaching [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 99f66ed9-3a75-4e38-ad7d-6c27cc3529a9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 290454026cc87819bf9ffcf73329bb562e3dc5a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62916751"
---
# <a name="upgrade-a-database-using-detach-and-attach-transact-sql"></a>使用分离和附加来升级数据库 (Transact-SQL)
  本主题说明如何使用分离和附加操作在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中升级数据库。 在附加到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]后，数据库将立即变为可用，然后会自动进行升级。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
-   **升级 SQL Server 数据库：**  
  
     [使用分离和附加操作](#SSMSProcedure)  
  
-   **跟进：**  [在升级 SQL Server 数据库后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   不能附加系统数据库。  
  
-   附加和分离操作可以通过将数据库的 **cross db ownership chaining** 选项设置为 0 来禁用数据库的跨数据库所有权链接。 有关启用链接的详细信息，请参阅 [cross db ownership chaining 服务器配置选项](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)。  
  
-   附加复制的而不是分离的复制数据库时：  
  
    -   如果将该数据库附加到同一服务器实例的升级版本中，则必须在附加操作完成后执行 **sp_vupgrade_replication** 来升级复制数据库。 有关详细信息，请参阅 [sp_vupgrade_replication (Transact SQL)](/sql/relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql)。  
  
    -   如果将该数据库附加到不同的服务器实例中（不考虑版本），则必须在附加操作完成后执行 **sp_removedbreplication** 来删除复制数据库。 有关详细信息，请参阅 [sp_removedbreplication (Transact SQL)](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)。  
  
###  <a name="Recommendations"></a> 建议  
 建议您不要附加或还原来自未知或不可信源的数据库。 此类数据库可能包含恶意代码，这些代码可能会执行非预期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，或者通过修改架构或物理数据库结构导致错误。 使用未知或不受信任的源中的数据库之前，请在非生产服务器上的数据库上运行[DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) ，并检查数据库中的代码，例如存储过程或其他用户定义的代码。  
  
##  <a name="SSMSProcedure"></a>使用分离和附加来升级数据库  
  
1.  分离数据库。 有关详细信息，请参阅[分离数据库](detach-a-database.md)。  
  
2.  （可选）移动所分离的数据库文件和日志文件。  
  
     即使希望创建新的日志文件，也应该将日志文件与数据文件一起移动。 在某些情况下，重新附加数据库需要使用其现有的日志文件。 因此，除非在不使用分离日志文件的情况下可以成功附加数据库，否则，请始终保留所有分离的日志文件。  
  
    > [!NOTE]  
    >  如果尝试在不指定日志文件的情况下附加数据库，则附加操作将会在日志文件的原始位置中查找文件。 如果该位置仍存在日志文件的原始副本，则附加该副本。 若要避免使用原始日志文件，请指定新日志文件的路径，或在日志文件复制到新位置之后，删除其原始副本。  
  
3.  将复制的文件附加到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的实例。 有关详细信息，请参阅[附加数据库](attach-a-database.md)。  
  
## <a name="example"></a>示例  
 以下实例升级以前版本的 SQL Server 的数据库副本。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句在与该服务器实例（附加该数据库副本）连接的查询编辑器窗口中执行。  
  
1.  执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句以分离数据库：  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'MyDatabase';  
    GO  
    ```  
  
2.  使用您选择的方法，将数据文件和日志文件复制到新位置。  
  
    > [!IMPORTANT]  
    >  对于生产数据库，请将数据库和事务日志存放在不同的磁盘上。  
  
     若要通过网络将文件复制到远程计算机的磁盘上，请使用远程位置的通用命名约定 (UNC) 名称。 ** \\ **UNC 名称采用的格式为_Servername_**\\**_共享_**\\**名_路径_**\\**_Filename_。 将文件写入本地硬盘时，必须对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例使用的用户帐户授予读写远程磁盘文件所需的相应权限。  
  
3.  通过执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句来附加移动的数据库及其日志（日志为可选项）：  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyDatabase   
        ON (FILENAME = 'C:\MySQLServer\MyDatabase.mdf'),  
        (FILENAME = 'C:\MySQLServer\Database.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，新附加的数据库在对象资源管理器中不是立即可见的。 若要查看数据库，请在对象资源管理器中，单击 **“查看”** ，再单击 **“刷新”**。 在对象资源管理器中展开 **“数据库”** 节点后，新附加的数据库即显示在数据库列表中。  
  
##  <a name="FollowUp"></a>跟进：在升级 SQL Server 数据库后  
 如果数据库具有全文检索，则升级过程将导入、重置或重新生成它们，具体取决于 **upgrade_option** 服务器属性的设置。 如果将升级选项设置为“导入”(**upgrade_option** = 2) 或“重新生成”(**upgrade_option** = 0)，在升级过程中将无法使用全文检索。 导入可能需要数小时，而重新生成所需的时间最多时可能十倍于此，具体取决于要编制索引的数据量。 另请注意，如果将升级选项设置为“导入”，并且全文目录不可用，则会重新生成关联的全文索引。 若要更改 **upgrade_option** 服务器属性的设置，请使用 [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)。  
  
### <a name="database-compatibility-level-after-upgrade"></a>升级后的数据库兼容级别  
 如果升级前用户数据库的兼容级别为 100 或更高，升级后将保持相应级别。 如果升级前兼容级别为 90，则在升级后的数据库中，兼容级别将设置为 100，该级别为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]支持的最低兼容级别。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。  
  
### <a name="managing-metadata-on-the-upgraded-server-instance"></a>管理已升级服务器实例上的元数据  
 将数据库附加到其他服务器实例时，为了给用户和应用程序提供一致的体验，您可能需要在其他服务器实例上为数据库重新创建部分或全部元数据（例如登录名、作业和权限）。 有关详细信息，请参阅 [当数据库在其他服务器实例上可用时管理元数据 (SQL Server)](manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
### <a name="service-master-key-and-database-master-key-encryption-changes-from-3des-to-aes"></a>服务主密钥和数据库主密钥加密从 3DES 更改为 AES  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本使用 AES 加密算法来保护服务主密钥（SMK）和数据库主密钥（DMK）。 AES 是一种比早期版本中使用的 3DES 更新的加密算法。 当数据库第一次附加或还原到新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例时，数据库主密钥（由服务主密钥加密）的副本尚未存储在服务器中。 必须使用 `OPEN MASTER KEY` 语句解密数据库主密钥 (DMK)。 一旦 DMK 解密后，通过使用 `ALTER MASTER KEY REGENERATE` 语句向服务器提供 DMK（使用服务主密钥 (SMK) 加密）的副本，即可拥有将来启用自动解密的选项。 当数据库已从较早版本升级后，应重新生成 DMK 以使用更新的 AES 算法。 有关重新生成 DMK 的详细信息，请参阅 [ALTER MASTER KEY (Transact-SQL)](/sql/t-sql/statements/alter-master-key-transact-sql)。 重新生成 DMK 密钥以升级到 AES 所需的时间取决于 DMK 保护的对象数。 重新生成 DMK 密钥以升级到 AES 只在必需时执行一次，不影响将来作为密钥循环策略的一部分而重新生成的过程。  
  
  
