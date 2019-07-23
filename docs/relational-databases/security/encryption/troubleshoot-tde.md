---
title: 使用 Azure Key Vault 中的客户托管密钥进行透明数据加密的常见错误 | Microsoft Docs
description: 使用 Azure Key Vault 配置来排除透明数据加密 (TDE) 故障。
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f67d1ed9bf809baaa4d934947e86d3fd1b7ed0b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111533"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>使用 Azure Key Vault 中的客户托管密钥进行透明数据加密的常见错误

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
本文介绍了使用 Azure Key Vault 中的客户托管密钥进行透明数据加密 (TDE) 的要求，以及如何发现和解决常见错误。

## <a name="requirements"></a>要求

若要使用 Key Vault 中的客户托管 TDE 保护程序来排除 TDE 故障，必须满足以下要求：

- 逻辑 SQL Server 实例和密钥保管库必须位于同一区域内。
- Azure Active Directory (Azure AD) 提供的逻辑 SQL Server 实例标识（即 Azure Key Vault 中的 AppId）必须是原始订阅中的租户。 如果服务器移到与创建位置不同的订阅中，必须重新创建服务器标识 (AppId)。
- 必须启动并运行密钥保管库。 若要了解如何检查密钥保管库状态，请参阅 [Azure 资源运行状况](https://docs.microsoft.com/azure/service-health/resource-health-overview)。 若要注册接收通知，请阅读有关[操作组](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups)的内容。
- 在异地灾难恢复方案中，两个密钥保管库必须包含相同的密钥材料，这样故障转移才能生效。
- 逻辑服务器必须有用于对密钥保管库进行身份验证的 Azure AD 标识 (AppId)。
- AppId 必须有权访问密钥保管库，并且必须对已选为 TDE 保护程序的密钥拥有“获取、包装和取消包装”权限。

有关详细信息，请参阅[使用 Azure Key Vault 配置 TDE 的指南](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault)。

## <a name="common-misconfigurations"></a>常见错误配置

使用 Key Vault 进行 TDE 时，发生的大多数问题都是由下列错误配置之一引起的：

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>密钥保管库不可用或不存在

- 密钥保管库遭意外删除。
- 为 Azure Key Vault 配置的防火墙禁止访问 Microsoft 服务。

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>无权访问密钥保管库或密钥不存在

- 密钥遭意外删除。
- 逻辑 SQL Server 实例 AppId 遭意外删除。
- 逻辑 SQL Server 实例移到其他订阅中。 如果逻辑服务器移到其他订阅中，必须新建 AppId。
- 向 AppId 授予的密钥权限不足（即不包括“获取、包装和取消包装”权限）。
- 逻辑 SQL Server 实例 AppId 的权限遭撤销。

## <a name="identify-and-resolve-common-errors"></a>发现和解决常见错误

此部分列出了最常见错误的疑难解答步骤。

### <a name="missing-server-identity"></a>缺少服务器标识

**错误消息**

401 AzureKeyVaultNoServerIdentity - 在服务器上配置的服务器标识不正确。  请联系支持人员。

**检测**

使用下面的 cmdlet 或命令，以确保已向逻辑 SQL Server 实例分配标识：

- Azure PowerShell：[Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 

- Azure CLI：[az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

**缓解**

使用下面的 cmdlet 或命令，以配置逻辑 SQL Server 实例的 Azure AD 标识 (AppId)：

- Azure PowerShell：[Set-AzureRmSqlServer](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0)（含 `-AssignIdentity` 选项）。

- Azure CLI：[az sql server update](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update)（含 `--assign_identity` 选项）。

在 Azure 门户中，依次转到密钥保管库和“访问策略”  。 完成以下步骤： 

 1. 使用“新增”  按钮，为上一步中创建的服务器添加 AppId。 
 1. 分配以下密钥权限：获取、包装、解包 

若要了解详细信息，请参阅[将 Azure AD 标识分配给服务器](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)。

> [!IMPORTANT]
> 如果在使用 Key Vault 对 TDE 进行初始配置后，逻辑 SQL Server 实例移到新订阅中，请重复 Azure AD 标识配置步骤，以新建 AppId。 然后，将 AppId 添加到密钥保管库，并向它分配正确的密钥权限。 
>

### <a name="missing-key-vault"></a>缺少密钥保管库

**错误消息**

503 AzureKeyVaultConnectionFailed - 无法在服务器上完成操作，因为尝试连接到 Azure Key Vault 失败。 

**检测**

若要标识密钥 URI 和密钥保管库，请执行以下操作：

1. 使用下面的 cmdlet 或命令，以获取具体逻辑 SQL Server 实例的密钥 URI：

    - Azure PowerShell：[Get-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

    - Azure CLI：[az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

1. 使用密钥 URI 来标识密钥保管库：

    - Azure PowerShell：可检查 $MyServerKeyVaultKey 变量的属性，以获取密钥保管库的详细信息。

    - Azure CLI：检查返回的服务器加密保护程序，以获取密钥保管库的详细信息。

**缓解**

确认密钥保管库是否可用：

- 确保密钥保管库可用，且逻辑 SQL Server 实例拥有访问权限。
- 如果密钥保管库位于防火墙后，请务必选中允许 Microsoft 服务访问密钥保管库的复选框。
- 如果密钥保管库已遭意外删除，必须从头开始完成配置。


### <a name="missing-key"></a>缺少密钥

**错误消息**

404 ServerKeyNotFound - 在当前订阅上找不到请求的服务器密钥。  

409 ServerKeyDoesNotExists - 服务器密钥不存在。 

**检测**

若要标识密钥 URI 和密钥保管库，请执行以下操作：

- 使用[缺少密钥保管库](#missing-key-vault)中的 cmdlet 或命令，以标识添加到逻辑 SQL Server 实例的密钥 URI。 运行这些命令会返回密钥列表。

**缓解**

确认密钥保管库中是否有 TDE 保护程序：

1. 标识密钥保管库，然后在 Azure 门户中转到密钥保管库。
1. 确保密钥 URI 标识的密钥存在。

### <a name="missing-permissions"></a>缺少权限

**错误消息**

401 AzureKeyVaultMissingPermissions - 服务器缺少对 Azure Key Vault 的必需权限。 

**检测**

若要标识密钥 URI 和密钥保管库，请执行以下操作： 

- 使用[缺少密钥保管库](#missing-key-vault)中的 cmdlet 或命令，以标识逻辑 SQL Server 实例使用的密钥保管库。

**缓解**

确认逻辑 SQL Server 实例是否有权访问密钥保管库，以及是否拥有正确的密钥访问权限：

- 在 Azure 门户中，依次转到密钥保管库和“访问策略”  。 查找逻辑 SQL Server 实例 AppId。  
- 如果 AppId 存在，请确保 AppID 拥有以下密钥权限：获取、包装和解包。
- 如果 AppID 不存在，请使用“新增”  按钮进行添加。 

## <a name="next-steps"></a>后续步骤

- 请参阅[使用 Azure Key Vault 配置 TDE 的指南](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault)。
- 了解 [Azure 资源运行状况](https://docs.microsoft.com/azure/service-health/resource-health-overview)。
- 回顾如何[将 Azure AD 标识分配给服务器](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)。
