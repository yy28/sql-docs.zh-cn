---
title: "TDE - 自带密钥 (BYOK) - Azure SQL | Microsoft Docs"
description: "SQL 数据库和数据仓库的 Azure Key Vault 中用于透明数据加密 (TDE) 的自带密钥 (BYOK) 支持。 支持 BYOK 的 TDE 的概述、优点、工作原理、注意事项和建议。"
keywords: 
services: sql-database
documentationcenter: 
author: aliceku
manager: craigg
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: 
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 01/31/2018
ms.author: aliceku
ms.openlocfilehash: 1fdb7da4fe1276a66494873fc38aa15ae67bae27
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="transparent-data-encryption-with-bring-your-own-key-preview-support-for-azure-sql-database-and-data-warehouse"></a>使用 Azure SQL 数据库和数据仓库的“创建自己的密钥”（预览）支持进行透明数据加密
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
- 选择所需资源将要使用的订阅 – 如果以后跨订阅移动服务器，则需要使用 BYOK 设置新的 TDE。
- 使用 BYOK 配置 TDE 时，必须考虑重复的包装/解包操作在密钥保管库中放置的负载。 例如，由于与逻辑服务器关联的所有数据库都使用相同的 TDE 保护程序，因此该服务器的故障转移触发针对保管库的密钥操作次数等于该服务器中的数据库数目。 根据我们的经验以及记录的[密钥保管库服务限制](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-service-limits)，建议在单个订阅中将最多 500 个标准数据库或 200 个高级数据库与一个 Azure Key Vault 关联，以确保在访问保管库中的 TDE 保护程序时实现一致的高可用性。 
- 建议：在本地保留 TDE 保护程序的副本。  这需要使用 HSM 设备在本地创建 TDE 保护程序和密钥托管系统，以存储 TDE 保护程序的本地副本。


### <a name="guidelines-for-configuring-azure-key-vault"></a>有关配置 Azure Key Vault 的准则

- 在启用[软删除](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)的情况下使用密钥保管库，以防密钥（或密钥保管库）意外删除时丢失数据：  
  - 被软删除的资源将保留一段时间（90 天），除非它们被恢复或清除。
  - “恢复”和“清除”操作具有与密钥保管库访问策略相关的各自权限。 
- 授予逻辑服务器权限，让其可以使用自己的 Azure Active Directory (AAD) 标识访问密钥保管库。  使用门户 UI 时会自动创建 AAD 标识，并向服务器授予密钥保管库的访问权限。  通过 PowerShell 使用 BYOK 配置 TDE，必须创建 AAD 标识，且应验证完成情况。 请参阅[使用 BYOK 配置 TDE](transparent-data-encryption-byok-azure-sql-configure.md)，获取使用 PowerShell 时的详细分步说明。

  >[!NOTE]
  >如果意外删除了 AAD 标识或者使用密钥保管库的访问策略撤销了服务器的权限，服务器就会失去访问密钥保管库的权限。
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

在第二种情况中，需要基于现有 SQL 数据库故障转移组或数据库的活动异地复制副本配置冗余 Azure Key Vault，从而保持 Azure Key Vault 中 TDE 保护程序的高可用性。  每个异地复制服务器都需要一个单独的密钥保管库，理想情况下和它们的服务器位于同一个 Azure 区域。 如果因为一个区域发生中断而无法访问主数据库，且触发了故障转移，则可以使用辅助密钥保管库让辅助数据库进行接管。  

![故障转移组和 geo-dr](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

若要在故障转移期间实现对 Azure Key Vault 中 TDE 保护程序的持续访问，则必须在复制数据库或故障转移至辅助服务器之前就对此进行配置。 主服务器和辅助服务器都必须存储所有其他 Azure Key Vault 中的 TDE 保护程序的副本，也就是说，在这个例子中，两个密钥保管库存储了相同的密钥。

若要将一个密钥保管库中的现有密钥添加至另一个密钥保管库，请使用 [Add-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) cmdlet。

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

若要消除此问题，请运行 [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) cmdlet，以返回已添加到服务器的 Key Vault 中的密钥列表（除非它们已被用户删除）。 若要保证可以还原所有备份，请确保用于备份的目标服务器有权访问所有这些密钥。

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
若要了解有关 SQL 数据库的备份恢复的详细信息，请参阅[恢复 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups)。 若要了解有关 SQL 数据仓库的备份恢复的详细信息，请参阅[恢复 Azure SQL 数据仓库](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview)。

已备份日志文件的其他注意事项：已备份日志文件仍使用原始 TDE 加密程序进行加密，即使 TDE 保护程序已轮换，数据库现在使用新的 TDE 保护程序也是如此。  在还原时，需要这两个密钥才能还原数据库。  如果日志文件使用存储在 Azure Key Vault 中的 TDE 保护程序，还原时需要此密钥，即使数据库此时已更改为使用服务托管的 TDE。   
