---
title: 备份加密 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 334b95a8-6061-4fe0-9e34-b32c9f1706ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2420e494a312f64ba84edbd9a77b26be2a53e33b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659325"
---
# <a name="backup-encryption"></a>备份加密
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题概述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份的加密选项。 其中详细介绍备份期间加密的用法、优点和推荐做法。  
  
  
##  <a name="Overview"></a> 概述  
 从 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]开始，SQL Server 可在创建备份时加密数据。 通过在创建备份时指定加密算法和加密程序（证书或非对称密钥），可创建加密的备份文件。 所有存储目标：支持本地和 Windows Azure 存储。 此外，可为 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 操作配置加密选项，这是 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中引入的一项新功能。  
  
 若要在备份期间加密，必须指定加密算法以及用于保护加密密钥的加密程序。 支持以下加密选项：  
  
-   **加密算法：** 支持的加密算法包括 AES 128、AES 192、AES 256 和 Triple DES  
  
-   **加密程序：** 证书或非对称密钥  
  
> [!CAUTION]  
>  备份证书或非对称密钥很重要，并且备份的位置最好与其用于加密的备份文件不同。 没有证书或非对称密钥，即无法还原备份，从而使备份文件无法重用。  
  
 **还原加密的备份：** SQL Server 还原不需要在还原期间指定任何加密参数。 但要求在要还原到的实例上有用于加密备份文件的证书或非对称密钥。 执行还原的用户帐户必须对证书或密钥具有 **VIEW DEFINITION** 权限。 如果将加密的备份还原到其他实例，则必须确保该实例上有证书。  
  
 如果从经过 TDE 加密的数据库还原备份，则要还原到的实例上应有 TDE 证书。  
  
##  <a name="Benefits"></a> 优点  
  
1.  加密数据库备份有助于保护数据：SQL Server 提供在创建备份的同时加密备份数据的选项。  
  
2.  加密还可用于使用 TDE 加密的数据库。  
  
3.  由 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]进行的备份支持加密，这样可提高站点外备份的安全性。  
  
4.  此功能支持多个最高 AES 256 位的加密算法。 这样可选择符合要求的算法。  
  
5.  可将加密密钥与扩展密钥管理 (EKM) 提供程序集成。  
  
  
##  <a name="Prerequisites"></a> 先决条件  
 以下是有关加密备份的先决条件：  
  
1.  **创建 master 数据库的数据库主密钥：** 数据库主密钥是一个对称密钥，用于保护数据库中证书和非对称密钥的私钥。 有关详细信息，请参阅 [SQL Server 和数据库加密密钥（数据库引擎）](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)。  
  
2.  创建用于备份加密的证书或非对称密钥。 有关创建证书的详细信息，请参阅 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)。 有关创建非对称密钥的详细信息，请参阅[创建非对称密钥 (Transact-SQL)](../../t-sql/statements/create-asymmetric-key-transact-sql.md)。  
  
    > [!IMPORTANT]  
    >  仅支持位于扩展密钥管理 (EKM) 中的非对称密钥。  
  
##  <a name="Restrictions"></a> 限制  
 以下限制适用于加密选项：  
  
-   如果使用非对称密钥加密备份数据，则仅支持位于 EKM 提供程序中的非对称密钥。  
  
-   SQL Server Express 和 SQL Server Web 不支持在备份期间进行加密。 但是，支持从加密的备份还原到 SQL Server Express 或 SQL Server Web 的实例。  
  
-   旧版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法读取加密的备份。  
  
-   加密的备份不支持追加到现有的备份集选项。  
  
  
##  <a name="Permissions"></a> Permissions  
 **若要加密备份或从加密的备份还原：**  
  
 需要对用于加密数据库备份的证书或非对称密钥具有**VIEW DEFINITION** 权限。  
  
> [!NOTE]  
>  不需要访问 TDE 证书即可备份或还原受 TDE 保护的数据库。  
  
##  <a name="Methods"></a> 备份加密方法  
 以下各节简要介绍在备份期间加密数据的步骤。 有关使用 Transact-SQL 加密备份的不同步骤的完整演练，请参阅 [创建加密的备份](../../relational-databases/backup-restore/create-an-encrypted-backup.md)。  
  
### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
 在以下任何对话框中，可在创建数据库的备份时加密备份。  
  
1.  [备份数据库（“备份选项”页）](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)在“备份选项”页上，可以选择“加密”，并指定加密算法和证书或非对称密钥以用于加密。  
  
2.  [使用维护计划向导](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure)选择某个备份任务后，可以在“定义备份()任务”页的“选项”选项卡上，选择“备份加密”，并指定加密算法和证书或密钥以用于加密。  
  
### <a name="using-transact-sql"></a>使用 Transact SQL  
 以下是示例 Transact-SQL 语句以加密备份文件：  
  
```sql  
BACKUP DATABASE [MYTestDB]  
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
  
```  
  
 有关完整 Transact-SQL 语法，请参阅 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)。  
  
### <a name="using-powershell"></a>使用 PowerShell  
 此示例创建加密选项并在 **Backup-SqlDatabase** cmdlet 中将它作为参数值以创建加密的备份。  
  
```  
C:\PS>$encryptionOption = New-SqlBackupEncryptionOption -Algorithm Aes256 -EncryptorType ServerCertificate -EncryptorName "BackupCert"  
```  
  
```  
C:\PS>Backup-SqlDatabase -ServerInstance . -Database "MyTestDB" -BackupFile "MyTestDB.bak" -CompressionOption On -EncryptionOption $encryptionOption  
```  
  
##  <a name="RecommendedPractices"></a> 推荐做法  
 将加密证书和密钥备份到安装实例的本地计算机以外的位置。 若要考虑灾难恢复情况，请考虑将证书和密钥存储到站点外位置。 没有用于加密备份的证书即无法还原加密的备份。  
  
 若要还原加密的备份，要还原到的实例上应有进行备份时使用的原始证书及匹配的指纹。 因此，不应在到期时续订或以任何方式更改证书。 续订可导致更改证书并触发指纹更改，从而使证书对于备份文件变为无效。 执行还原的帐户应对备份期间用于加密的证书或非对称密钥具有 VIEW DEFINITION 权限。  
  
 可用性组数据库备份通常在首选备份副本上执行。  如果在不是备份来源的其他副本上还原备份，请确保用于备份的原始证书在还原到的副本上可用。  
  
 如果数据库启用了 TDE，则选择其他证书或非对称密钥用于加密数据库和备份以提高安全性。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
|主题/任务|描述|  
|-----------------|-----------------|  
|[创建加密的备份](../../relational-databases/backup-restore/create-an-encrypted-backup.md)|介绍创建加密的备份所需的基本步骤|  
|[使用 Azure Key Vault 的可扩展密钥管理 (SQL Server)](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)|提供了创建受 Azure 密钥保管库中的密钥保护的加密备份的示例。|  
  
## <a name="see-also"></a>另请参阅  
 [备份概述 (SQL Server)](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  
