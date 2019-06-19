---
title: 使用 Azure 密钥保管库 (AKV) 中客户托管的密钥进行透明数据加密 (TDE) 的常见错误和解决方法 | Microsoft Docs
description: 使用 Azure 密钥保管库配置对透明数据加密 (TDE) 进行问题排查。
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
manager: craigg
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 1366d0a20ed39b466d1a2f6cb3e84f0f30e17f9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718084"
---
# <a name="common-errors-and-resolutions-with-transparent-data-encryption-tde-with-customer-managed-keys-in-azure-key-vault-akv"></a>使用 Azure 密钥保管库 (AKV) 中客户托管的密钥进行透明数据加密 (TDE) 的常见错误和解决方法

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
本主题提供有关以下问题的信息：  
  
- 要求  
- 如何确定和解决最常见的错误

## <a name="requirements"></a>要求
若要[使用 AKV 配置中客户托管的 TDE 保护程序对 TDE 进行问题排查](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault)，请首先确认以下要求：
- 逻辑 SQL Server 和密钥保管库需要位于同一区域。
- Azure Active Directory 提供的逻辑 SQL Server 标识（Azure 密钥保管库中的 APPID）被限制为原始订阅中的租户。  如果服务器被移动到另一个订阅，则必须重新创建服务器标识 (APPID)。
- 需要启动并运行密钥保管库，了解 [Azure 资源运行状况](https://docs.microsoft.com/azure/service-health/resource-health-overview)以检查密钥保管库状态，并了解[操作组](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups)以注册通知。
- 在 Geo-DR 方案中，两个密钥保管库必须包含相同的密钥材料，然后才能进行故障转移。
- 逻辑服务器需要具有 Azure Active Directory (AAD) 标识 (APPID)，以便对密钥保管库进行身份验证。
- APPID 需要能够访问密钥保管库以及包装和解包，并且需要获取被选为 TDE 保护程序的密钥的权限。

通过 AKV 使用 TDE 时遇到的大多数问题均由以下某种错误配置引起：

### <a name="key-vault-unavailable-or-doesnt-exist"></a>密钥保管库不可用或不存在？
- 密钥保管库被意外删除
- 为 Azure 密钥保管库配置的防火墙不允许访问 Microsoft 服务

### <a name="no-permissions-to-access-the-key-vault-or-key-doesnt-exist"></a>不存在任何访问密钥保管库或密钥的权限？
- 密钥被意外删除
- SQL APPID 被意外删除
- SQL 被移动到其他订阅，需要新的 APPID
- 为 APPID 授予的密钥权限不足（包装、解包、获取）
- SQL APPID 权限被撤销


在下一部分中，我们将列出最常见错误的排查步骤。


## <a name="how-to-identify-and-resolve-the-most-common-errors"></a>如何确定和解决最常见的错误

## <a name="missing-server-identity"></a>缺少服务器标识
错误消息：“401 AzureKeyVaultNoServerIdentity - 在服务器上配置的服务器标识不正确。 请联系支持人员。”

检测：使用以下命令确保已向逻辑 SQL Server 分配标识：

- [Azure PowerShell Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 
- [Azure CLI az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

缓解：为逻辑 SQL Server 配置 Azure Active Directory (Azure AD) 标识 (APPID)

对于 PowerShell：使用带有选项 [-AssignIdentity](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) 的 Set-AzureRmSqlServer 命令 

对于 CLI：使用带有选项 [--assign_identity](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) 的 az sql server update 命令 

在 Azure 门户中，浏览到密钥保管库并转到访问策略：  
 - 使用“新增”按钮，为上一步中创建的服务器添加 APPID。 
 - 分配以下密钥权限：获取、包装、解包 

[了解更多信息](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)

> [!IMPORTANT]
> 如果在使用 AKV 对 TDE 进行初始配置后，逻辑 SQL Server 被移动到新的订阅，则必须重复进行配置 AAD 标识的步骤才能创建新的 APPID。  然后需要将新 APPID 添加到密钥保管库，并且需要重新分配正确的权限。 
>

## <a name="missing-key-vault"></a>缺少密钥保管库
错误消息：“503 AzureKeyVaultConnectionFailed - 无法在服务器上完成操作，因为尝试连接到 Azure Key Vault 失败”

检测：如何识别密钥 URI 和密钥保管库 

第 1 步：使用以下命令获取给定逻辑 SQL Server 的密钥 URI：

-[Azure PowerShell get-azurermsqlserverkeyvaultkey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

-[Azure CLI az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

第 2 步：使用密钥 URI 标识密钥保管库

PowerShell：可检查 $MyServerKeyVaultKey 的属性，获取有关密钥保管库的详细信息

CLI：检查返回的服务器加密保护程序，获取有关密钥保管库的详细信息

缓解：确认密钥保管库可用
- 确保密钥保管库可用且逻辑 SQL Server 具有访问权限
- 如果密钥保管库位于防火墙后，请确保勾选“允许 Microsoft 服务访问密钥保管库”的复选框
- 如果密钥保管库被意外删除，则必须从头开始完成配置


## <a name="missing-key"></a>缺少密钥 
错误消息：“404 ServerKeyNotFound - 未在当前订阅上找到请求的服务器密钥。”
“409 ServerKeyDoesNotExists - 服务器密钥不存在。”

检测：如何识别密钥 URI 和密钥保管库
- 使用上一节“缺少密钥保管库”中的 cmdlet 标识添加到逻辑 SQL Server 的密钥 URI，以返回密钥列表。

缓解：确认 AKV 中存在 TDE 保护程序
- 标识密钥保管库，并在 Azure 门户中浏览到它
- 确保存在密钥 URI 标识的密钥

## <a name="missing-permissions"></a>缺少权限 
错误消息：“401 AzureKeyVaultMissingPermissions - 服务器缺少 Azure Key Vault 的必需权限。”

检测：如何识别密钥 URI 和密钥保管库
- 使用“缺少密钥保管库”一节中的 cmdlet 标识逻辑 SQL Server 使用的密钥保管库。

缓解：确认逻辑 SQL Server 具有密钥保管库权限以及访问密钥的正确权限
- 在 Azure 门户中，浏览到密钥保管库，转到访问策略，找到 SQL Server APPID：  
  - 如果 APPID 不存在，请使用“新增”按钮进行添加。 
  - 如果 APPID 存在，请确保它具有以下密钥权限：获取、包装和解包。
