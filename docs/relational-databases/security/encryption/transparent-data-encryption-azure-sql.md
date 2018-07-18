---
title: 用于 Azure SQL 数据库和数据仓库的透明数据加密 | Microsoft Docs
description: 概述用于 SQL 数据库和数据仓库的透明数据加密。 本文档介绍了其优点和配置选项，包括服务托管的透明数据加密和自带密钥。
keywords: ''
author: becczhang
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.date: 07/09/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 49a3745e67a51ee8f5eb9625d518328f61593514
ms.sourcegitcommit: dcd29cd2d358bef95652db71f180d2a31ed5886b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2018
ms.locfileid: "37934849"
---
# <a name="transparent-data-encryption-for-sql-database-and-data-warehouse"></a>用于 SQL 数据库和数据仓库的透明数据加密
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

透明数据加密 (TDE) 有助于保护 Azure SQL 数据库和 Azure 数据仓库免受恶意活动的威胁。 它对数据库、关联备份和静态事务日志文件执行实时加密和解密，且无需更改应用程序。 默认情况下，为所有新部署的 Azure SQL 数据库启用 TDE。 TDE 不能用于加密 SQL 数据库中的逻辑主数据库。  主数据库包含对用户数据库执行 TDE 操作所需的对象。

需要为较旧的数据库或 Azure SQL 数据仓库手动启用 TDE。  

透明数据加密使用称为数据库加密密钥 (DEK) 的对称密钥对整个数据库的存储进行加密。 此数据库加密密钥受透明数据加密保护程序保护。 该保护程序可以是服务托管的证书（服务托管的透明数据加密），也可以是存储在 Azure Key Vault 中的非对称密钥（“自带密钥”）。 在服务器级别设置透明数据加密保护程序。 

数据库启动时，已加密的数据库加密密钥被解密，然后用于解密和重新加密 SQL Server 数据库引擎进程中的数据库文件。 透明数据加密可在页面级别对数据执行实时 I/O 加密和解密。 在将每个页面读取到内存时进行解密，在写入磁盘之前进行加密。 有关透明数据加密的一般说明，请参阅[透明数据加密](transparent-data-encryption.md)。

在 Azure 虚拟机上运行的 SQL Server 也可以使用 Key Vault 的非对称密钥。 配置步骤不同于使用 SQL 数据库中的非对称密钥。 有关详细信息，请参阅 [使用 Azure Key Vault 的可扩展密钥管理 (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md)。

## <a name="service-managed-transparent-data-encryption"></a>服务托管的透明数据加密

在 Azure 中，透明数据加密的默认设置是数据库加密密钥受内置服务器证书保护。 内置服务器证书对每个服务器而言是唯一的。 如果数据库为异地复制关系，主数据库和异地辅助数据库均受主数据库的父级服务器密钥保护。 如果两个数据库连接到同一台服务器，则它们共享相同的内置证书。 Microsoft 至少每 90 天自动轮换这些证书。

Microsoft 也可无缝移动和管理异地复制和还原所需的密钥。 

> [!IMPORTANT]
> 默认情况下，使用服务托管的透明数据加密对所有新创建的 SQL 数据库进行加密。 默认情况下，不加密 2017 年 5 月之前的现有数据库和通过还原、异地复制和数据库副本创建的数据库。
>

## <a name="bring-your-own-key"></a>自带密钥

借助自带密钥支持，用户可以控制其透明数据加密密钥，并能控制访问人员和访问时间。 Key Vault 是基于Azure 云的外部密钥管理系统，是第一个透明数据加密将其与自带密钥支持集成的密钥管理服务。 借助自带密钥支持，数据库加密密钥可受存储在 Key Vault 中的非对称密钥的保护。 非对称密钥始终位于 Key Vault 中。 服务器拥有密钥保管库权限后，服务器会通过 Key Vault 向它发送基本的密钥操作请求。 在服务器级别设置非对称密钥，则该服务器下的所有数据库都会继承该密钥。

借助自带密钥支持，现在可以控制密钥轮替和密钥保管库权限等密钥管理任务。 还可以删除密钥并对所有加密密钥启用审核/报告。 Key Vault 提供中央密钥管理，并使用严密监控的硬件安全模块。 Key Vault 促进密钥和数据管理的分离，有助于符合法规遵从性。 若要了解有关 Key Vault 的详细信息，请参阅 [Key Vault 文档页](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。

若要了解有关使用 SQL 数据库和数据仓库的自带密钥支持进行透明数据加密的详细信息，请参阅[使用自带秘钥支持进行透明数据加密](transparent-data-encryption-byok-azure-sql.md)。

若要通过自带秘钥支持开始使用透明数据加密，请访问操作指南[通过 PowerShell 使用 Key Vault 的自有密钥启用透明数据加密](transparent-data-encryption-byok-azure-sql-configure.md)。

## <a name="move-a-transparent-data-encryption-protected-database"></a>移动由透明数据加密保护的数据库

不需要为 Azure 中的操作解密数据库。 在目标数据库上，以透明方式继承源数据库或主数据库上的透明数据加密设置。 其中包括的操作涉及以下方面：
- 地域恢复。
- 自助式时间点还原。
- 还原已删除数据库。
- 活动异地复制。
- 创建数据库副本。

导出由透明数据加密保护的数据库时，数据库的导出内容不会加密。 此导出内容存储在未加密的 BACPAC 文件中。 完成新数据库的导入后，请务必适当保护 BACPAC 文件并启用透明数据加密。

例如，如果从本地 SQL Server 实例中导出 BACPAC 文件，则不会自动加密新数据库的导入内容。 同样，如果将 BACPAC 文件导出到本地 SQL Server 实例，也不会自动加密新数据库。

导入 Azure SQL 数据库和从中导出的情况例外。 在新数据库中启用了透明数据加密，但 BACPAC 文件本身仍未加密。

## <a name="manage-transparent-data-encryption-in-the-azure-portal"></a>在 Azure 门户中管理透明数据加密

若要通过 Azure 门户配置透明数据加密，用户必须作为 Azure 所有者、参与者或 SQL 安全管理员进行连接。 

在数据库级别设置透明数据加密。 若要对数据库启用透明数据加密，请访问 [Azure 门户](https://portal.azure.com)并使用 Azure 管理员或参与者帐户登录。 在用户数据库下找到透明数据加密设置。 默认情况下，使用服务托管的透明数据加密。 自动为包含该数据库的服务器生成透明数据加密证书。 

![服务托管的透明数据加密](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

在服务器级别设置透明数据加密主密钥（也称为透明数据加密保护程序）。 若要通过自带密钥支持使用透明数据加密并使用 Key Vault 中的密钥保护数据库，请参阅服务器下的透明数据加密设置。 

![使用自带密钥支持的透明数据加密](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="manage-transparent-data-encryption-by-using-powershell"></a>使用 PowerShell 管理透明数据加密

若要通过 PowerShell 配置透明数据加密，用户必须作为 Azure 所有者、参与者或 SQL 安全管理员进行连接。 

| Cmdlet | 描述 |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |启用或禁用数据库的透明数据加密|
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |获取数据库的透明数据加密状态 |
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption-Activity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |检查数据库的加密进度 |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |将 Key Vault 密钥添加到 SQL Server 实例 |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |获取 SQL Server 实例的 Key Vault 密钥  |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |设置 SQL Server 实例的透明数据加密保护程序 |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |获取透明数据加密保护程序 |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |将 Key Vault 密钥从 SQL Server 实例中删除 |
|  | |

## <a name="manage-transparent-data-encryption-by-using-transact-sql"></a>使用 Transact-SQL 管理透明数据加密

使用管理员或主数据库中 dbmanager 角色成员的登录名连接到数据库。

| Command | 描述 |
| --- | --- |
| [ALTER DATABASE（Azure SQL 数据库）](/sql/t-sql/statements/alter-database-azure-sql-database) | SET ENCRYPTION ON/OFF 可加密或解密数据库 |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |返回与数据库加密状态以及相关联数据库加密密钥有关的信息 |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |返回与每个数据仓库节点的加密状态及其关联数据库加密密钥有关的信息 | 
|  | |

无法使用 Transact-SQL 将透明数据加密保护程序切换为 Key Vault 中的密钥。 使用 PowerShell 或 Azure 门户。

## <a name="manage-transparent-data-encryption-by-using-the-rest-api"></a>使用 REST API 管理透明数据加密
 
若要通过 REST API 配置透明数据加密，用户必须作为 Azure 所有者、参与者或 SQL 安全管理员进行连接。 

| Command | 描述 |
| --- | --- |
|[创建或更新服务器](/rest/api/sql/servers/createorupdate)|将 Azure Active Directory 标识添加到 SQL Server 实例（用于授予对 Key Vault 的访问权限）|
|[创建或更新服务器密钥](/rest/api/sql/serverkeys/createorupdate)|将 Key Vault 密钥添加到 SQL Server 实例|
|[删除服务器密钥](/rest/api/sql/serverkeys/delete)|将 Key Vault 密钥从 SQL Server 实例中删除|
|[获取服务器密钥](/rest/api/sql/serverkeys/get)|从 SQL Server 实例获取特定的 Key Vault 密钥|
|[按服务器列出服务器密钥](/rest/api/sql/serverkeys/listbyserver)|获取 SQL Server 实例的 Key Vault 密钥 |
|[创建或更新加密保护程序](/rest/api/sql/encryptionprotectors/createorupdate)|设置 SQL Server 实例的透明数据加密保护程序|
|[获取加密保护程序](/rest/api/sql/encryptionprotectors/get)|获取 SQL Server 实例的透明数据加密保护程序|
|[按服务器列出加密保护程序](/rest/api/sql/encryptionprotectors/listbyserver)|获取 SQL Server 实例的透明数据加密保护程序 |
|[创建或更新透明数据加密配置](/rest/api/sql/transparentdataencryptions/createorupdate)|启用或禁用数据库的透明数据加密|
|[获取透明数据加密配置](/rest/api/sql/transparentdataencryptions/get)|获取数据库的透明数据加密配置|
|[列出透明数据加密配置结果](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|获取数据库的加密结果|

## <a name="next-steps"></a>后续步骤

- 有关透明数据加密的一般说明，请参阅[透明数据加密](transparent-data-encryption.md)。
- 若要了解有关使用 SQL 数据库和数据仓库的自带密钥支持进行透明数据加密的详细信息，请参阅[使用自带秘钥支持进行透明数据加密](transparent-data-encryption-byok-azure-sql.md)。
- 若要通过自带密钥支持开始使用透明数据加密，请访问操作指南[通过 PowerShell 使用 Key Vault 的自带密钥启用透明数据加密](transparent-data-encryption-byok-azure-sql-configure.md)。
- 有关 Key Vault 的详细信息，请参阅 [Key Vault 文档页](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。
