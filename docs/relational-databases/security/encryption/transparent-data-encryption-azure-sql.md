---
title: "Azure SQL 数据库和数据仓库的 TDE | Microsoft Docs"
description: "SQL 数据库和数据仓库的透明数据加密的概述。 本文档介绍了其优点和配置选项，包括服务托管的 TDE 和自带密钥。"
keywords: 
author: becczhang
manager: craigg
editor: 
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.custom: 
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.openlocfilehash: a3fee8259aab2901eaf7950d4255d78d1860eeda
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="transparent-data-encryption-for-azure-sql-database-and-data-warehouse"></a>用于 Azure SQL 数据库和数据仓库的透明数据加密
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

透明数据加密 (TDE) 对数据库、关联的备份和事务日志文件执行实时静态加密和解密，而无需更改应用程序，从而帮助保护 Azure SQL 数据库和数据仓库免受恶意活动的威胁。

TDE 使用称为数据库加密密钥 (DEK) 的对称密钥加密整个数据库的存储。 此数据库加密密钥受 TDE 保护程序保护，可以是服务托管证书（“服务托管 TDE”），也可以是存储在 Azure Key Vault 中的非对称密钥（“自带密钥”）。 TDE 保护程序设置为服务器级别。 

在数据库启动时，已加密的 DEK 被解密，然后用于解密和重新加密 SQL 引擎进程中的数据库文件。 TDE 对页面级数据执行实时 I/O 加密和解密。 每个页面在读取到内存时被解密，在写入磁盘之前被加密。 有关 TDE 的一般说明，请参阅[透明数据加密 (TDE)](transparent-data-encryption.md)。

在 Azure 虚拟机上运行的 SQL Server 也可以使用 Key Vault 的非对称密钥。 配置步骤不同于使用 Azure SQL 数据库中的非对称密钥。 有关详细信息，请参阅 [使用 Azure Key Vault 的可扩展密钥管理 (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md)。

## <a name="service-managed-tde"></a>服务托管 TDE

在 Azure 中，TDE 的默认设置是数据库加密密钥受内置服务器证书保护。 内置服务器证书对每个服务器而言是唯一的。 如果数据库为异地复制关系，主要数据库和异地辅助数据库均受主要数据库的父级服务器密钥保护。 如果 2 个数据库连接到同一台服务器，则它们共享相同的内置证书。 Microsoft 至少每 90 天自动轮换这些证书。

Microsoft 也可无缝移动和管理异地复制和还原所需的密钥。 

> [!IMPORTANT]
> 默认情况下使用服务托管 TDE 加密所有新创建的 SQL 数据库。 默认情况下不加密 2017 年 5 月之前的现有数据库和通过还原、异地复制和数据库副本创建的数据库。
>

## <a name="bring-your-own-key"></a>自带密钥

通过自带密钥 (BYOK) 支持，用户能够控制其 TDE 加密密钥以及访问人员和访问时间。 Azure Key Vault (AKV) 是 Azure 的基于云的外部密钥管理系统，是第一个 TDE 将其与 BYOK 支持集成的密钥管理服务。 使用 BYOK 时，数据库加密密钥受存储在 AKV 中的非对称密钥保护。 非对称密钥绝不会离开 Key Vault；一旦服务器拥有密钥保管库权限，服务器会通过 Key Vault 服务向它发送基本的密钥操作请求。 非对称密钥设置为服务器级别，并由该服务器下的所有数据库继承该密钥。 通过使用 BYOK 支持，用户现可控制密钥管理任务（包括密钥轮换、密钥保管库权限、删除密钥），并且可以对所有加密密钥启用审核/报告。 Key Vault 提供中心密钥管理，利用严格监控的硬件安全模块 (HSM)，并促进分离密钥和数据的管理以帮助满足监管符合性。 若要了解有关 Key Vault 的详细信息，请访问[Key Vault 文档页](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。

若要了解有关使用 Azure SQL 数据库和数据仓库的 BYOK 支持进行 TDE 的详细信息，请参阅[使用自带秘钥支持进行透明数据加密](transparent-data-encryption-byok-azure-sql.md)。

若要通过 BYOK 支持开始使用 TDE，请访问操作指南[通过 PowerShell 使用 Key Vault 的自有密钥启用透明数据加密](transparent-data-encryption-byok-azure-sql-configure.md)。

## <a name="moving-a-tde-protected-database"></a>移动 TDE 保护的数据库

不需要为 Azure 中的操作解密数据库。 源数据库或主数据库上 TDE 的设置均以透明方式继承在目标系统上。 这包括涉及以下内容的操作：
- 地域恢复
- 自服务时点还原
- 还原已删除数据库
- 活动异地复制
- 创建数据库副本

在导出受 TDE 保护的数据库时，不会加密数据库的导出内容。 此导出内容存储在未加密的 BACPAC 文件中。 完成新数据库的导入后，请务必适当保护 BACPAC 文件并启用 TDE。

例如，如果从本地 SQL Server 中导出 BACPAC 文件，则不会自动加密新数据库的导入内容。 同样，如果将 BACPAC 文件导出到本地 SQL Server，也不会自动加密新数据库。

一个例外情况是导出到 Azure SQL 数据库和从 Azure SQL 数据库导出。 在新数据库中启用了 TDE，但 PACPAC 文件本身仍未加密。

## <a name="managing-transparent-data-encryption-in-the-azure-portal"></a>在 Azure 门户中管理透明数据加密

若要通过 Azure 门户配置 TDE，用户必须作为 Azure 所有者、参与者或 SQL 安全管理员进行连接。 

透明数据加密设置为数据库级别。 若要对数据库启用 TDE，请访问 [Azure 门户](https://portal.azure.com)并使用 Azure 管理员或参与者帐户登录。 在用户数据库下查找 TDE 设置。 默认情况下，使用服务托管 TDE，并为包含数据库的服务器自动生成 TDE 证书。 

![服务托管 TDE](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

TDE 主密钥，也称为 TDE 保护程序，设置为服务器级别。 若要使用自带秘钥进行 TDE 和使用 Azure Key Vault 的密钥保护数据库，请访问服务器下的 TDE 设置。 

![使用 BYOK 支持的 TDE](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="managing-transparent-data-encryption-using-powershell"></a>使用 PowerShell 管理透明数据加密

若要通过 PowerShell 配置 TDE，用户必须作为 Azure 所有者、参与者或 SQL 安全管理员进行连接。 

| Cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |启用或禁用数据库的 TDE。|
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |获取数据库的 TDE 状态。 |
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption-Activity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |检查数据库的加密进度。 |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |将 Key Vault 密钥添加到 SQL 服务器。 |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |获取 SQL 服务器的 Key Vault 密钥。 |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |设置 SQL 服务器的 TDE 保护程序。 |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |获取透明数据加密 (TDE) 保护程序。 |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |将 Key Vault 密钥从 SQL 服务器中删除。 |
|  | |

## <a name="managing-transparent-data-encryption-using-transact-sql"></a>管理使用 Transact-SQL 的透明数据加密

使用管理员或主数据库中 dbmanager 角色成员的登录名连接到数据库。

| Command | Description |
| --- | --- |
| [ALTER DATABASE（Azure SQL 数据库）](/sql/t-sql/statements/alter-database-azure-sql-database) | 使用 SET ENCRYPTION ON/OFF 加密或解密数据库。 |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |返回与数据库加密状态以及相关联数据库加密密钥有关的信息。 |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |返回与每个数据仓库节点的加密状态及其关联数据库加密密钥有关的信息。 | 
|  | |

不能使用 Transact-SQL 将 TDE 保护程序切换到 Azure Key Vault 的密钥；请使用 PowerShell 或 Azure 门户。

## <a name="managing-transparent-data-encryption-using-rest-api"></a>使用 REST API 管理透明数据加密
 
若要通过 REST API 配置 TDE，用户必须作为 Azure 所有者、参与者或 SQL 安全管理员进行连接。 

| Command | Description |
| --- | --- |
|[创建或更新服务器](/rest/api/sql/servers/createorupdate)|将 AAD 标识添加到 SQL 服务器（用于授予 Key Vault 的访问权限）。|
|[创建或更新服务器密钥](/rest/api/sql/serverkeys/createorupdate)|将 Key Vault 密钥添加到 SQL 服务器。|
|[删除服务器密钥](/rest/api/sql/serverkeys/delete)|将 Key Vault 密钥从 SQL 服务器中删除。|
|[获取服务器密钥](/rest/api/sql/serverkeys/get)|从 SQL 服务器获取特定的 Key Vault 密钥。|
|[按服务器列出服务器密钥](/rest/api/sql/serverkeys/listbyserver)|获取 SQL 服务器的 Key Vault 密钥。|
|[创建或更新加密保护程序](/rest/api/sql/encryptionprotectors/createorupdate)|设置 SQL 服务器的 TDE 保护程序。|
|[获取加密保护程序](/rest/api/sql/encryptionprotectors/get)|获取 SQL 服务器的 TDE 保护程序。|
|[按服务器列出加密保护程序](/rest/api/sql/encryptionprotectors/listbyserver)|获取 SQL 服务器的 TDE 保护程序。|
|[创建或更新透明数据加密配置](/rest/api/sql/transparentdataencryptions/createorupdate)|启用或禁用数据库的 TDE。|
|[获取透明数据加密配置](/rest/api/sql/transparentdataencryptions/get)|获取数据库的 TDE 配置。|
|[列出透明数据加密配置结果](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|获取数据库的加密结果。|

## <a name="next-steps"></a>后续步骤

- 有关 TDE 的一般说明，请参阅[透明数据加密 (TDE)](transparent-data-encryption.md)。

- 若要了解有关使用 Azure SQL 数据库和数据仓库的 BYOK 支持进行 TDE 的详细信息，请访问[使用自带秘钥支持进行透明数据加密](transparent-data-encryption-byok-azure-sql.md)。

- 若要通过 BYOK 支持开始使用 TDE，请访问操作指南[通过 PowerShell 使用 Key Vault 的自有密钥启用透明数据加密](transparent-data-encryption-byok-azure-sql-configure.md)。

- 有关 Key Vault 的详细信息，请参阅 [Key Vault 文档页](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。
