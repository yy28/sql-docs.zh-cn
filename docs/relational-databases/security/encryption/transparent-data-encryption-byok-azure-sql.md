---
title: TDE - 自带密钥 (BYOK) - Azure SQL | Microsoft Docs
description: SQL 数据库和数据仓库的 Azure Key Vault 中用于透明数据加密 (TDE) 的自带密钥 (BYOK) 支持。 支持 BYOK 的 TDE 的概述、优点、工作原理、注意事项和建议。
keywords: ''
services: sql-database
documentationcenter: ''
author: aliceku
manager: craigg
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.date: 06/28/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 1b738239cca6b1afa543718ef64831f72b6490e0
ms.sourcegitcommit: 3e5f1545e5c6c92fa32e116ee3bff1018ca946a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2018
ms.locfileid: "37107235"
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>使用 Azure SQL 数据库和数据仓库的自带密钥支持进行透明数据加密
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

通过支持[透明数据加密 (TDE)](transparent-data-encryption.md) 的“创建自己的密钥”(BYOK) 功能，可以使用称为“TDE 保护程序”的非对称密钥对数据库加密密钥 (DEK) 进行加密。  TDE 保护程序存储在你控制下的 [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)（Azure 基于云的外部密钥管理系统）中。 Azure Key Vault 是第一个 TDE 将其与 BYOK 支持集成的密钥管理服务。 TDE DEK 存储在数据库的引导页上，由 TDE 保护程序进行加密和解密。 TDE 保护程序存储在 Azure Key Vault 中，且绝不会离开密钥保管库。 如果服务器对密钥保管库的访问权限被撤销，则无法将数据库解密和读取进内存。  在逻辑服务器级别设置 TDE 保护程序，并且由与服务器关联的所有数据库继承。 

结合 BYOK 支持，用户现可控制密钥管理任务（包括密钥轮换、密钥保管库权限、删除密钥），并可使用 Azure Key Vault 功能对所有 TDE 保护程序启用审核/报告。 Key Vault 提供中心密钥管理，利用严格监控的硬件安全模块 (HSM)，并支持分离密钥和数据管理之间的职责以帮助满足监管符合性。  


使用 BYOK 的 TDE 具有下列优点：
- 提高了透明度和细化控制能力，能够自助管理 TDE 保护程序   
- 因为在 Key Vault 中承载，所以可以集中管理 TDE 保护程序（以及在其他 Azure 服务中使用的其他密钥和机密）
- 在组织内分离密钥和数据的管理责任，以支持职责分离
- 使用自己的客户端，更值得信赖。因为 Key Vault 旨在避免 Microsoft 看到或提取任何加密密钥。 
- 支持密钥轮换

> [!IMPORTANT]
> 对于使用服务托管 TDE 并想要开始使用 Key Vault 的用户来说，TDE 在切换到 Key Vault 的 TDE 保护程序的过程中保持启用状态。 数据库文件本身不停机，也不会重新加密。 从服务托管的密钥切换到 Key Vault 密钥只需要重新加密数据库加密密钥 (DEK)，这是一个快速的在线操作。 
>

## <a name="how-does-tde-with-byok-support-work"></a>使用 BYOK 支持的 TDE 是如何工作的？
 
![向 Key Vault 验证服务器](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

当 TDE 首次配置为使用 Key Vault 的 TDE 保护程序时，服务器将每个启用 TDE 的数据库的 DEK 发送到 Key Vault，以获得 wrap key 请求。 Key Vault 返回存储在用户数据库中的加密数据库加密密钥。  

>[!IMPORTANT]
>请务必注意，TDE 保护程序存储在 Azure Key Vault 以后就绝不会离开。 逻辑服务器只能将密钥操作请求发送到 Key Vault 内的 TDE 保护程序密钥材料，并且绝不会访问或缓存 TDE 保护程序。 Key Vault 管理员有权随时撤销服务器的 Key Vault 权限，在这种情况下所有到服务器的连接都被截断。 
>


## <a name="guidelines-for-configuring-tde-with-byok"></a>有关配置使用 BYOK 的 TDE 的准则

### <a name="general-guidelines"></a>通用指导原则
- 确保 Azure Key Vault 和 Azure SQL 数据库将在同一个租户中。  不支持跨租户的密钥保管库和服务器交互。
- 选择所需资源将要使用的订阅 – 如果以后跨订阅移动服务器，则需要使用 BYOK 设置新的 TDE。 详细了解[移动资源](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-move-resources)
- 使用 BYOK 配置 TDE 时，必须考虑重复的包装/解包操作在密钥保管库中放置的负载。 例如，由于与逻辑服务器关联的所有数据库都使用相同的 TDE 保护程序，因此该服务器的故障转移触发针对保管库的密钥操作次数等于该服务器中的数据库数目。 根据我们的经验以及记录的[密钥保管库服务限制](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-service-limits)，建议在单个订阅中将最多 500 个标准数据库/常规用途数据库或 200 个高级数据库/业务关键数据库与一个 Azure Key Vault 关联，以确保在访问保管库中的 TDE 保护程序时实现一致的高可用性。 
- 建议：在本地保留 TDE 保护程序的副本。  这需要使用 HSM 设备在本地创建 TDE 保护程序和密钥托管系统，以存储 TDE 保护程序的本地副本。


### <a name="guidelines-for-configuring-azure-key-vault"></a>有关配置 Azure Key Vault 的准则

- 在启用[软删除](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)的情况下创建密钥保管库，以防密钥（或密钥保管库）意外删除时丢失数据。  必须使用 [PowerShell 启用密钥保管库中的“软删除”属性](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell)（该选项在从 AKV 门户中尚不可用，但 SQL 需要该选项）：  
  - 被软删除的资源将保留一段时间（90 天），除非它们被恢复或清除。
  - “恢复”和“清除”操作具有与密钥保管库访问策略相关的各自权限。 
- 对密钥保管库设置资源锁，以控制谁能够删除此关键资源，并帮助防止意外或未经授权的删除。  [详细了解资源锁](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-lock-resources)

- 授予逻辑服务器权限，让其可以使用自己的 Azure Active Directory (Azure AD) 标识访问密钥保管库。  使用门户 UI 时会自动创建 Azure AD 标识，并向服务器授予密钥保管库的访问权限。  通过 PowerShell 使用 BYOK 配置 TDE，必须创建 Azure AD 标识，且应验证完成情况。 请参阅[使用 BYOK 配置 TDE](transparent-data-encryption-byok-azure-sql-configure.md)，获取使用 PowerShell 时的详细分步说明。

  >[!NOTE]
  >如果意外删除了 Azure AD 标识或者使用密钥保管库的访问策略撤销了服务器的权限，服务器就会失去访问密钥保管库的权限。
  >
  
- 为所有加密密钥启用审核和报告：Key Vault 提供了可轻松注入到其他安全信息和事件管理 (SIEM) 工具的日志。 Operations Management Suite (OMS) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) 是一个已集成的示例服务。
- 要确保已加密数据库的高可用性，请为每个逻辑服务器配置两个位于不同区域的 Azure Key Vault。


### <a name="guidelines-for-configuring-the-tde-protector-asymmetric-key-stored-in-azure-key-vault"></a>有关配置存储在 Azure Key Vault 中的 TDE 保护程序（非对称密钥）的准则

- 在本地 HSM 设备上以本地方式创建加密密钥。 确保此密钥是一个非对称的 RSA 2048 密钥，以便将其存储在 Azure Key Vault 中。
- 将密钥托管在密钥托管系统中。  
- 将加密密钥文件（.pfx、.byok 或 .backup）导入 Azure Key Vault。 
    

>[!NOTE] 
    >出于测试目的，可以使用 Azure Key Vault 创建一个密钥，但是无法托管该密钥，因为专用密钥绝不能离开密钥保管库。  务必备份并托管用于加密生产数据的密钥，因为密钥丢失（密钥保管库中的意外删除、过期等等）会导致永久性的数据丢失。
    >
    
- 使用没有到期日期的密钥 – 也不要为任何使用中的密钥设置到期日期：密钥一旦过期，加密数据库就会失去对 TDE 保护程序的访问权限，并会在 24 小时内被删除。
- 确保密钥已启用且具备执行 get、wrap key 和 unwrap key 操作的权限。
- 在首次使用 Azure Key Vault 中的密钥之前，先创建 Azure Key Vault 密钥备份。 了解有关 [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) 命令的详细信息。
- 每次更改密钥（例如添加 ACL、添加标记以及添加密钥属性）时，请创建新的备份。
- 在密钥轮换期间，在密钥保管库中保留以前版本的密钥，以便可以恢复旧的数据库备份。 当数据库的 TDE 保护程序发生了更改，此数据库的旧备份不会为了使用最新的 TDE 保护程序而进行更新。  恢复每个备份都需要用到创建它的 TDE 保护程序。 按照[使用 PowerShell 轮换透明数据加密保护程序](transparent-data-encryption-byok-azure-sql-key-rotation.md)中的说明，可以执行密钥轮换。
- 改回服务托管密钥后，将以前用过的所有密钥保留至 Azure Key Vault。  这样可以确保数据库备份能通过存储在 Azure Key Vault 中的 TDE 保护程序进行恢复。  必须对使用 Azure Key Vault 创建的 TDE 保护程序进行维护，直到使用服务托管密钥创建了所有存储的备份。  
- 使用 [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) 生成这些密钥的可恢复备份副本。
- 若要在没有数据丢失风险的情况下，删除可能已在安全事件中泄露的密钥，请遵循[删除可能已泄露的密钥](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)中的步骤。


## <a name="high-availability-geo-replication-and-backup--restore"></a>高可用性、异地复制和备份/还原

### <a name="high-availability-and-disaster-recovery"></a>高可用性和灾难恢复

使用 Azure Key Vault 配置高可用性的方式取决于数据库和逻辑服务器的配置，下面是针对两种不同情况的推荐配置。  第一种情况是独立数据库或逻辑服务器（未配置异地冗余）。  第二种情况是配置了故障转移组或异地冗余的数据库或逻辑服务器，这种情况必须确保每个异地冗余副本的故障转移组中都有本地 Azure Key Vault 来保障异地故障转移的运行。 在第一种情况中，如果需要未配置异地冗余的数据库或逻辑服务器具备高可用性，那么最好将服务器配置为使用具有相同密钥材料且处于两个不同区域的两个不同密钥保管库。  为此，请使用和逻辑服务器位于同一区域的主密钥保管库创建 TDE 保护程序，并将密钥克隆至位于不同 Azure 区域的密钥保管库，这样一来，如果主密钥保管库在数据库启用并运行时出现中断，服务器就可以访问第二个密钥保管库。 使用 Backup-AzureKeyVaultKey cmdlet 在主密钥保管库中以加密格式检索密钥，然后使用 Restore-AzureKeyVaultKey cmdlet 并在第二个区域中指定一个密钥保管库。


![单一服务器 HA 且没有 geo-dr](./media/transparent-data-encryption-byok-azure-sql/SingleServer_HA_Config.PNG)

## <a name="how-to-configure-geo-dr-with-azure-key-vault"></a>如何使用 Azure Key Vault 配置 Geo-DR

要保持用于加密数据库的 TDE 保护程序的高可用性，需要基于现有的或所需的 SQL 数据库故障转移组或活动异地复制实例配置冗余 Azure Key Vault。  每个异地复制服务器都需要一个单独的 Key Vault，该 Key Vault 必须与服务器位于同一个 Azure 区域。 如果因为一个区域发生中断而无法访问主数据库，且触发了故障转移，则可以使用辅助密钥保管库让辅助数据库进行接管。 
 
对于异地复制的 Azure SQL 数据库，需要以下 Azure Key Vault 配置：
- 区域中需要有一个具有 Key Vault 的主数据库和一个具有 Key Vault 的辅助数据库。 
- 至少需要一个辅助数据库，最多支持四个辅助数据库。 
- 不支持链式辅助数据库。

以下部分将详细说明安装和配置步骤。 

### <a name="azure-key-vault-configuration-steps"></a>Azure Key Vault 配置步骤

- 安装 [PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0) 
- 使用 Key Vault 中的 [PowerShell 启用“软删除”属性](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell)，在两个不同区域创建两个 Azure Key Vault（该选项在 AKV 门户中还不可用，但 SQL 需要该选项）。
- 这两个 Azure Key Vault 都必须位于在相同 Azure 地域中可用的两个区域，才能备份和恢复密钥。  如果需要将两个 Key Vault 位于不同地区以满足 SQL Geo-DR 要求，请遵循 [BYOK 过程](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-hsm-protected-keys)，该过程允许从本地 HSM 导入密钥。
- 在第一个 Key Vault 中创建新的密钥：  
  - RSA/RSA HSA 2048 密钥 
  - 永久有效 
  - 密钥已启用且具备执行 get、wrap key 和 unwrap key 操作的权限 
- 备份主密钥，并将该密钥还原到第二个 Key Vault 中。  请参阅 [BackupAzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) 和 [Restore-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey?view=azurermps-5.5.0)。 

### <a name="azure-sql-database-configuration-steps"></a>Azure SQL 数据库配置步骤

无论从新的 SQL 部署开始，还是使用现有的 SQL Geo-DR 部署，以下配置步骤都不相同。  我们首先概述新部署的配置步骤，然后说明如何将存储在 Azure Key Vault 中的 TDE 保护程序分配到已创建 Geo-DR 链接的现有部署。 

新部署的步骤：
- 在与之前创建的 Key Vault 相同的两个区域中创建两个逻辑 SQL Server。 
- 选择逻辑服务器 TDE 窗格，并用于每个逻辑 SQL Server：  
   - 在相同区域中选择 AKV 
   - 选择密钥用作 TDE 保护程序 - 每个服务器都将使用该 TDE 保护程序的本地副本。 
   - 在门户中执行此操作将为逻辑 SQL Server（用于分配访问 Key Vault 的逻辑 SQL Server 权限）创建 [AppID](https://docs.microsoft.com/en-us/azure/active-directory/managed-service-identity/overview)，请勿删除此标识符。 而对于逻辑 SQL Server（用于分配访问 Key Vault 的逻辑 SQL Server 权限），可通过删除 Azure Key Vault 中的权限来撤销访问。
- 创建主数据库。 
- 请按照[活动异地复制指南](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview)完成方案，此步骤将创建辅助数据库。

![故障转移组和 geo-dr](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

>[!NOTE]
>请务必先确保两个 Key Vault 显示相同的 TDE 保护程序，再继续创建数据库之间的异地链接。
>

针对已配置 Geo-DR 的现有 SQL DB 部署的步骤：

因为已存在逻辑 SQL Server，并已分配主数据库和辅助数据库，所以配置 Azure Key Vault 的步骤必须按照以下顺序执行： 
- 从托管辅助数据库的逻辑 SQL Server 开始： 
   - 分配位于相同区域的 Key Vault 
   - 分配 TDE 保护程序 
- 现在转到托管主数据库的逻辑 SQL Server： 
   - 选择与辅助 DB 使用的相同的 TDE 保护程序
   
![故障转移组和 geo-dr](./media/transparent-data-encryption-byok-azure-sql/geo_DR_ex_config.PNG)

>[!NOTE]
>将 Key Vault 分配到服务器时，请务必从辅助服务器开始。  在第二步中，将 Key Vault 分配到主服务器并升级 TDE 保护程序时，Geo-DR 链接将继续工作，因为此时复制的数据库使用的 TDE 保护程序对两台服务器都可用。
>

使用 Azure Key Vault 中客户托管的密钥为 SQL 数据库 Geo-DR 方案启用 TDE 之前，请务必保证在同一区域创建和维护具有相同内容的两个 Azure Key Vault，该区域将用于 SQL 数据库异地复制。  “相同内容”特指这两个 Key Vault 都必须包含相同的 TDE 保护程序副本，以便两个服务器都具有对所有数据库使用的 TDE 保护程序的访问权限。  具体而言，两个 Key Vault 必须保持同步，即密钥轮替之后它们必须包含 TDE 保护程序的相同副本，并保留用于日志文件或备份的旧版密钥，TDE 保护程序必须保持相同的密钥属性，而 Key Vault 必须保持对 SQL 同样的访问权限。  
 
请按照[活动异地复制概述](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)中的步骤测试和触发故障转移，应定期执行此操作以确认保留了 SQL 对两个 Key Vault 的访问权限。 


### <a name="backup-and-restore"></a>备份和还原

通过使用 Key Vault 密钥的 TDE 对数据库加密后，所有生成的备份也使用相同的 TDE 保护程序进行加密。

若要还原使用 Key Vault 的 TDE 保护程序加密的备份，请确保密钥材料仍在原密钥名称下的原保管库中。 当数据库的 TDE 保护程序发生了更改，此数据库的旧备份不会为了使用最新的 TDE 保护程序而进行更新。 因此，建议保留 Key Vault 中的 TDE 保护程序的所有旧版本，以便可以还原数据库备份。 

如果可能需要用于还原备份的密钥不再处于其原密钥保管库中，将返回以下错误消息：“目标服务器 <Servername> 无法访问创建于 <Timestamp #1> 和 <Timestamp #2>.之间的所有 AKV Uri。 请在还原所有 AKV Uri 后重试操作。”

若要消除此问题，请运行 [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) cmdlet，以返回已添加到服务器的 Key Vault 中的密钥列表（除非它们已被用户删除）。 若要保证可以还原所有备份，请确保用于备份的目标服务器有权访问所有这些密钥。

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
若要了解有关 SQL 数据库的备份恢复的详细信息，请参阅[恢复 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups)。 若要了解有关 SQL 数据仓库的备份恢复的详细信息，请参阅[恢复 Azure SQL 数据仓库](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview)。


已备份日志文件的其他注意事项：已备份日志文件仍使用原始 TDE 加密程序进行加密，即使 TDE 保护程序已轮换，数据库现在使用新的 TDE 保护程序也是如此。  在还原时，需要这两个密钥才能还原数据库。  如果日志文件使用存储在 Azure Key Vault 中的 TDE 保护程序，还原时需要此密钥，即使数据库此时已更改为使用服务托管的 TDE。


