---
title: "TDE - 自带密钥 - Azure SQL |Microsoft Docs"
description: "SQL 数据库和数据仓库的 Azure Key Vault 中用于透明数据加密的自带密钥的概述。 本文档介绍此功能的优点、它的工作原理、注意事项以及建议。"
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: cguyer
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.openlocfilehash: 35e51899bda60ccb5b176de0a3d7fabcc86faad7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>使用 Azure SQL 数据库和数据仓库的自带密钥支持进行透明数据加密

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

用于[透明数据加密 (TDE)](transparent-data-encryption.md) 的自带密钥 (BYOK) 支持允许用户控制其 TDE 加密密钥以及访问人员和访问时间。 [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault) 是 Azure 的基于云的外部密钥管理系统，是第一个 TDE 将其与 BYOK 支持集成的密钥管理服务。 使用 BYOK 时，数据库加密密钥受存储在 Key Vault 中的非对称密钥保护。 非对称密钥设置为服务器级别，并由该服务器下的所有数据库继承该密钥。 

通过使用 BYOK 支持，用户现可控制密钥管理任务（包括密钥轮换、密钥保管库权限、删除密钥），并且可以对所有加密密钥启用审核/报告。 Key Vault 提供中心密钥管理，利用严格监控的硬件安全模块 (HSM)，并促进分离密钥和数据的管理以帮助满足监管符合性。 

使用 BYOK 的 TDE 具有下列优点：
- 提高了透明度和细化控制能力，能够自助管理 TDE 保护程序   
- 因为在 Key Vault 中承载，可以集中管理 TDE 加密密钥（以及在其他其他 Azure 服务中使用的其他密钥和机密）
- 在组织内分离密钥和数据的管理，以支持角色分离
- 使用自己的客户端，更值得信赖。因为 Key Vault 旨在避免 Microsoft 看到或提取任何加密密钥。 
- 支持密钥轮换

> [!IMPORTANT]
> 对于使用服务托管 TDE 并想要开始使用 Key Vault 的用户来说，TDE 在切换到 Key Vault 的密钥过程中保持启用状态。 数据库文件本身不停机，也不会重新加密。 从服务托管的密钥切换到 Key Vault 密钥需要重新加密数据库加密密钥，这是一个快速的在线操作。
>

## <a name="how-does-tde-with-byok-support-work"></a>使用 BYOK 支持的 TDE 是如何工作的？
 
![向 Key Vault 验证服务器](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

当 TDE 配置为使用 Key Vault 的密钥时，服务器将每个启用 TDE 的数据库的数据库加密密钥发送到 Key Vault，以获得 wrap key请求。 Key Vault 返回存储在用户数据库中的加密数据库加密密钥。 

请务必注意，密钥存储在 Key Vault 后，该密钥不再离开 Key Vault。 Key Vault 中由硬件安全模块 (HSM) 支持的密钥不会离开 HSM 安全边界。 服务器只能将密钥操作请求发送到 Key Vault 内的 TDE 保护程序密钥材料。 Key Vault 管理员有权随时撤销服务器的 Key Vault 权限，在这种情况下所有到服务器的连接都被截断。 

## <a name="considerations"></a>注意事项

通过使用 BYOK 的 TDE 可带来其他密钥管理任务和使用密钥保管库本身的相关成本。 接下来的两个部分讨论了这些注意事项。

### <a name="key-management-responsibilities"></a>密钥管理职责

接管应用程序资源的加密密钥管理是一项很重要的职责。 通过 Key Vault 将 BYOK 用于 TDE，以下是假定的密钥管理任务：
- 密钥轮换：TDE 保护程序应根据内部规定或符合性要求轮换。 密钥轮换可以通过 TDE 保护程序的密钥保管库完成。  
- 密钥保管库权限：Key Vault 内跨密钥保管库和服务器级别预配的权限。 密钥保管库的服务器权限可以随时使用密钥保管库的访问策略撤销。
- 删除键：密钥可能从 Key Vault 和 SQL 服务器中删除，以获取更多安全性或满足符合性。
- 审核/报告所有加密密钥：Key Vault 提供了可轻松注入到其他安全信息和事件管理 (SIEM) 工具的日志。 Operations Management Suite (OMS) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) 是一个已集成的示例服务。

### <a name="pricing-considerations"></a>定价注意事项 

使用 BYOK 支持的 TDE 是一项内置于 Azure SQL 数据库和数据仓库的安全功能，无需任何额外费用。 但是，使用 Key Vault 本身会产生相关费用。 服务器进行的 Key Vault 操作作为保管库的正常操作进行计费，遵循 Key Vault 的[定价](https://azure.microsoft.com/pricing/details/key-vault/)。 服务器将用于以下事件的请求发送到 Key Vault：
- SQL 实例重新启动
- 密钥滚动更新
- 每 6 个小时检查服务器的密钥保管库权限是否发生了任何更改

## <a name="important-warnings"></a>严重警告

### <a name="loss-of-access-to-keys"></a>无法访问密钥

一旦服务器（不论是通过删除 Key Vault 权限或已删除的密钥）无法再访问 TDE 保护程序，在服务器下的所有加密数据库连接都受到阻止，这些数据库会脱机并在 24 小时内被删除。 使用不可用的密钥加密的旧备份将无法再访问。 如果在极端情况下，密钥怀疑被泄露（使得服务或用户未经授权可访问密钥），最好的方法是通过[删除可能被泄露的密钥](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)中的以下指南删除密钥。 在删除活动的 TDE 保护程序之前必须删除数据库，可防止最多 10 分钟的数据丢失。  

### <a name="expired-keys"></a>已过期的密钥

因为 TDE 保护程序的可用性直接影响数据库可用性，所以含过期日期的密钥不能添加到 SQL 服务器。 如果已经密钥用作服务器的 TDE 保护程序，后来又添加了 Azure Key Vault 中的过期数据，一旦密钥过期，加密的数据库将无法再访问其 TDE 保护程序，并会在 24 小时内删除。

### <a name="deleted-server-identities"></a>已删除的服务器标识 

服务器对 Key Vault 的访问权限是通过服务器的唯一 Azure Active Directory (AAD) 标识管理的。 所以，如果服务器的标识从 AAD 中删除，服务器无法访问其密钥保管库。 因此，服务器下的所有加密数据库的连接都受到阻止，这些数据库会脱机并在 24 小时内删除。

## <a name="limitations"></a>限制

正用于 TDE 的密钥保管库必须与 SQL 数据库或数据仓库服务器处于相同的 AAD 租户。 不支持跨租户的密钥保管库和服务器交互。 正在使用 Key Vault 的密钥加密的资源不能跨 Azure 订阅移动。 跨订阅移动资源会破坏必要的 Key Vault 访问控制，导致无法使用 BYOK 进行 TDE。 如果必须将资源移动到另一个订阅，请将 TDE 模式从 BYOK 更改为[服务托管 TDE](transparent-data-encryption-azure-sql.md)。 

不支持数据库或数据仓库的唯一 TDE 保护程序。 TDE 保护程序设置为服务器级别，并由服务器下的所有资源继承。 

## <a name="guidelines-for-managing-encrypted-databases"></a>管理加密的数据库的指南

### <a name="high-availability-and-disaster-recovery"></a>高可用性和灾难恢复
  
有两种方法可以使用 Key Vault 为服务器配置异地复制： 

- 单独的密钥保管库：每个服务器有权访问单独的密钥保管库（理想情况下在各自的 Azure 区域内都有一个）。 这是推荐的配置，因为每个服务器自己具有用于加密异地复制数据库的 TDE 保护程序副本。 如果其中一个服务器的 Azure 区域处于脱机状态，其他服务器可以继续访问异地复制数据库。   

- 共享的密钥保管库：所有服务器共享相同的密钥保管库。 此配置更易于设置，但如果密钥保管库所在的 Azure 区域处于脱机状态，所有服务器都无法读取加密异地复制数据库或他们自己的加密数据库。 
 
开始时，请使用 [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) cmdlet 将每个服务器的 Key Vault 密钥添加到异地复制链接中的其他服务器。  
（Key Vault 的 KeyId 示例：*https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h*

   ```powershell
   <# Include the version guid in the KeyId #>
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

>[!NOTE]
>密钥保管库名称和密钥名称的组合字符长度不能超过 94 个字符。
>

按照[活动异地复制概述](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)中的步骤来使用这些服务器配置活动异地复制并触发故障转移。  

### <a name="backup-and-restore"></a>备份和还原

通过使用 Key Vault 密钥的 TDE 对数据库加密后，所有生成的备份也使用相同的 TDE 保护程序进行加密。

若要还原使用 Key Vault 的 TDE 保护程序加密的备份，请确保密钥材料仍在原密钥名称下的原保管库中。 当数据库的 TDE 保护程序发生了更改，此数据库的旧备份不会为了使用最新的 TDE 保护程序而进行更新。 因此，建议保留 Key Vault 中的 TDE 保护程序的所有旧版本，以便可以还原数据库备份。 

如果可能需要用于还原备份的密钥不再处于其原密钥保管库中，将返回以下错误消息：“目标服务器 <Servername> 无法访问创建于 <Timestamp #1> 和 <Timestamp #2>.之间的所有 AKV Uri。 请在还原所有 AKV Uri 后重试操作。”

若要消除此问题，请运行 [Get AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) cmdlet，以返回已添加到服务器的 Key Vault 中的密钥列表。 若要保证可以还原所有备份，请确保用于备份的目标服务器有权访问所有这些密钥。

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
若要了解有关 SQL 数据库的备份恢复的详细信息，请参阅[恢复 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups)。 若要了解有关 SQL 数据仓库的备份恢复的详细信息，请参阅[恢复 Azure SQL 数据仓库](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview)。

## <a name="best-practices"></a>最佳做法

### <a name="key-management"></a>密钥管理 

若要确保快速恢复密钥并访问 Azure 外的数据，建议采用以下做法：
- 在本地 HSM 设备上以本地方式创建加密密钥。 （确保此密钥是一个非对称的 RSA 2048 密钥，以便将其存储在 Azure Key Vault 中。）
- 将加密密钥文件（.pfx、.byok 或 .backup）导入 Azure Key Vault。 考虑使用已启用[软删除](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)的密钥保管库，以对意外密钥删除执行恢复保护。
- 在首次使用 Azure 密钥保管库中的密钥之前，先进行 Azure 密钥保管库密钥备份。 了解有关 [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) 命令的详细信息。
- 每次更改密钥（例如添加 ACL、添加标记、添加密钥属性）时，务必再进行一次 Azure Key Vault 密钥备份。
- 在密钥变换期间，在密钥保管库中保留以前版本的密钥，以便可以恢复旧的数据库备份。 

强烈建议首先在本地创建 TDE 加密密钥和对生产情况导入非对称密钥，因为这样管理员就可以在密钥托管系统中托管密钥。 如果非对称密钥是在 Azure Key Vault 中创建的，则无法托管，因为私钥不能离开保管库。 应托管用于保护关键数据的密钥。 丢失非对称密钥将导致数据永久性不可恢复。

### <a name="pre-configuration-for-replicated-databases"></a>复制数据库的预配置

如果加密的数据库将复制到另一个服务器，请确保服务器在移动或复制数据库之前有权访问在另一个服务器中使用的 Key Vault 密钥材料的副本。  

建议每个服务器都能有权访问在另一个服务器中使用的 Key Vault 密钥材料的副本，该副本存储在单独的密钥保管库中（理想情况下每个副本与服务器处于相同的 Azure 区域内）。 使用该设置，每个服务器自己具有用于加密复制数据库的 TDE 保护程序副本。 如果其中一个服务器的 Azure 区域处于脱机状态，其他服务器可以继续访问复制数据库。

## <a name="next-steps"></a>后续步骤

- 开始使用 TDE 的自带密钥支持：[通过 PowerShell 使用 Key Vault 的自有密钥启用 TDE](transparent-data-encryption-byok-azure-sql-configure.md)
- 了解如何轮换服务器的 TDE 保护程序以符合安全要求：[使用 PowerShell 轮换透明数据加密保护程序](transparent-data-encryption-byok-azure-sql-key-rotation.md)
- 如果存在安全风险，了解如何删除可能已泄露的 TDE 保护程序：[删除可能已泄露的密钥](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) 
