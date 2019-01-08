---
title: 可扩展的密钥管理 (EKM) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 42ec76542ffdf382c10c48cd107765d312ed1781
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375779"
---
# <a name="extensible-key-management-ekm"></a>可扩展的密钥管理 (EKM)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供数据加密功能以及*可扩展的密钥管理* (EKM)，同时使用“Microsoft 加密 API”(MSCAPI) 提供程序进行加密和生成密钥。 在临时密钥容器中可创建用于数据和密钥加密的加密密钥，并且必须先将它们从访问接口中导出，然后才能存储在数据库中。 这种方法使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]能够对密钥进行管理，其中包括加密密钥层次结构和密钥备份。  
  
 随着法规遵从性和数据隐私问题方面的需求不断增长，组织正利用加密方法来提供“深度防御”解决方案。 如果仅使用数据库加密管理工具，则这种方法通常是不切实际的。 硬件供应商通过使用“硬件安全模块”(HSM) 来提供能解决企业密钥管理的产品。 HSM 设备在硬件或软件模块上存储加密密钥。 由于加密密钥与加密数据分开存储，因此这是一种更安全的解决方案。  
  
 许多供应商提供 HSM 来解决密钥管理和加密加速问题。 HSM 设备对服务器进程使用硬件接口作为应用程序与 HSM 之间的媒介。 供应商还在他们的模块（可能是硬件或软件）上实施 MSCAPI 访问接口。 MSCAPI 通常只提供由 HSM 提供的功能子集。 供应商也可以针对 HSM、密钥配置和密钥访问提供管理软件。  
  
 HSM 的实现随供应商的不同而有所不同，将其用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 需要一个公共接口。 尽管 MSCAPI 提供此接口，但它仅支持 HSM 功能的子集。 另外它还存在其他限制，例如无法在本机保留对称密钥，以及缺少面向会话的支持。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可扩展的密钥管理能够使第三方 EKM/HSM 供应商在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中注册他们的模块。 注册后， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用户可以使用存储在 EKM 模块上的加密密钥。 这样， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 便可访问这些模块支持的高级加密功能（例如批量加密和解密）以及密钥管理功能（例如密钥老化和密钥旋转）。  
  
 当在 Azure VM 中运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以使用存储在 [Azure 密钥保管库](https://go.microsoft.com/fwlink/?LinkId=521401)中的密钥。 有关详细信息，请参阅 [使用 Azure Key Vault 的可扩展密钥管理 (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md)能够对密钥进行管理，其中包括加密密钥层次结构和密钥备份。  
  
## <a name="ekm-configuration"></a>EKM 配置  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的所有版本中都未提供可扩展密钥管理。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 默认情况下，可扩展的密钥管理是关闭的。 若要启用此功能，请使用包含以下选项和值的 sp_configure 命令，如下面的示例所示：  
  
```  
sp_configure 'show advanced', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'EKM provider enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
> [!NOTE]  
>  如果在不支持 EKM 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本中使用此选项的 sp_configure 命令，将会收到一条错误。  
  
 若要禁用该功能，请将此值设置为 **0**。 有关如何设置服务器选项的详细信息，请参阅 [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)。  
  
## <a name="how-to-use-ekm"></a>如何使用 EKM  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可扩展的密钥管理能够使保护数据库文件的加密密钥存储在即用型设备中，例如智能卡、USB 设备或 EKM/HSM 模块。 这样还能针对数据库管理员（除 sysadmin 组中的成员）来保护数据。 可以通过使用只能由数据库用户通过外部 EKM/HSM 模块访问的加密密钥来实现数据加密。  
  
 可扩展的密钥管理还提供下列优点：  
  
-   其他授权检查（启用责任分离）。  
  
-   更高性能的基于硬件的加密/解密。  
  
-   外部加密密钥生成。  
  
-   外部加密密钥存储（物理分离数据和密钥）。  
  
-   加密密钥检索。  
  
-   外部加密密钥保留（启用加密密钥旋转）。  
  
-   更易于加密密钥恢复。  
  
-   可管理的加密密钥分发。  
  
-   安全的加密密钥处置。  
  
 您可以对用户名和密码的组合或由 EKM 驱动程序定义的其他方法使用可扩展的密钥管理。  
  
> [!CAUTION]  
>  若要进行故障排除， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 技术支持可能需要 EKM 访问接口的加密密钥。 您可能还需要访问供应商工具或进程，以帮助解决问题。  
  
### <a name="authentication-with-an-ekm-device"></a>使用 EKM 设备进行身份验证  
 EKM 模块可以支持多种类型的身份验证。 每个访问接口只向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]公开一种身份验证类型，也就是说，如果模块支持“基本”或“其他”身份验证类型，则接口将公开这两种类型中的一种，而不会同时公开这两种类型。  
  
#### <a name="ekm-device-specific-basic-authentication-using-usernamepassword"></a>使用用户名/密码的 EKM 设备特定的基本身份验证  
 对于那些支持使用用户名/密码对的基本身份验证的 EKM 模块，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供使用凭据的透明身份验证。 有关凭据的详细信息，请参阅[凭据（数据库引擎）](../authentication-access/credentials-database-engine.md)。  
  
 可以为 EKM 访问接口创建凭据并将其映射到登录名（Windows 帐户和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帐户），以便根据每个登录名访问 EKM 模块。 凭据的 *Identify* 字段包含用户名； *secret* 字段包含连接到 EKM 模块的密码。  
  
 如果 EKM 访问接口没有任何登录映射的凭据，则使用映射到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户的凭据。  
  
 一个登录帐户可以映射多个凭据，只要它们用于不同的 EKM 访问接口即可。 每个 EKM 访问接口的每个登录名只能存在一个映射的凭据。 相同的凭据可以映射到其他登录名。  
  
#### <a name="other-types-of-ekm-device-specific-authentication"></a>其他类型的 EKM 设备特定的身份验证  
 对于身份验证不是采用 Windows 或用户/密码组合的 EKM 模块，必须单独从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 执行身份验证。  
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>通过 EKM 设备的加密和解密  
 下述功能和特性可用于通过对称和非对称密钥来加密和解密数据：  
  
|功能|参考|  
|-------------------------|---------------|  
|对称密钥加密|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)|  
|非对称密钥加密|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)|  
|EncryptByKey(key_guid, 'cleartext', ...)|[ENCRYPTBYKEY (Transact-SQL)](/sql/t-sql/functions/encryptbykey-transact-sql)|  
|DecryptByKey(ciphertext, ...)|[DECRYPTBYKEY (Transact-SQL)](/sql/t-sql/functions/decryptbykey-transact-sql)|  
|EncryptByAsmKey(key_guid, 'cleartext')|[ENCRYPTBYASYMKEY (Transact-SQL)](/sql/t-sql/functions/encryptbyasymkey-transact-sql)|  
|DecryptByAsmKey(ciphertext)|[DECRYPTBYASYMKEY (Transact-SQL)](/sql/t-sql/functions/decryptbyasymkey-transact-sql)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>通过 EKM 密钥的数据库密钥加密  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以使用 EKM 密钥加密数据库中的其他密钥。 您可以在 EKM 设备上同时创建和使用对称密钥和非对称密钥。 您可以使用 EKM 非对称密钥来加密本机（非 EKM）对称密钥。  
  
 下面的示例将创建一个数据库对称密钥并使用 EKM 模块上的密钥对其进行加密。  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
  
 有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中数据库和服务器密钥的详细信息，请参阅 [SQL Server 和数据库加密密钥（数据库引擎）](sql-server-and-database-encryption-keys-database-engine.md)。  
  
> [!NOTE]  
>  您不能使用一个 EKM 密钥来加密另一个 EKM 密钥。  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不支持对具有从 EKM 提供程序生成的非对称密钥的模块签名。  
  
## <a name="related-tasks"></a>Related Tasks  
 [EKM provider enabled 服务器配置选项](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
  
 [使用 EKM 启用 TDE](enable-tde-on-sql-server-using-ekm.md)  
  
 [使用 Azure 密钥保管库的可扩展密钥管理 (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [DROP CRYPTOGRAPHIC PROVIDER (Transact-SQL)](/sql/t-sql/statements/drop-cryptographic-provider-transact-sql)   
 [ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)](/sql/t-sql/statements/alter-cryptographic-provider-transact-sql)   
 [sys.cryptographic_providers (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql)   
 [sys.dm_cryptographic_provider_sessions (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-sessions-transact-sql)   
 [sys.dm_cryptographic_provider_properties (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql)   
 [sys.dm_cryptographic_provider_algorithms (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-algorithms-transact-sql)   
 [sys.dm_cryptographic_provider_keys (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-keys-transact-sql)   
 [sys.credentials (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [ALTER ASYMMETRIC KEY (Transact-SQL)](/sql/t-sql/statements/alter-asymmetric-key-transact-sql)   
 [DROP ASYMMETRIC KEY (Transact-SQL)](/sql/t-sql/statements/drop-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [ALTER SYMMETRIC KEY (Transact-SQL)](/sql/t-sql/statements/alter-symmetric-key-transact-sql)   
 [DROP SYMMETRIC KEY (Transact-SQL)](/sql/t-sql/statements/drop-symmetric-key-transact-sql)   
 [OPEN SYMMETRIC KEY (Transact-SQL)](/sql/t-sql/statements/open-symmetric-key-transact-sql)   
 [备份和还原 Reporting Services 加密密钥](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [删除和重新创建加密密钥（SSRS 配置管理器）](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [添加和删除扩展部署的加密密钥（SSRS 配置管理器）](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [备份服务主密钥](service-master-key.md)   
 [还原服务主密钥](restore-the-service-master-key.md)   
 [创建数据库主密钥](create-a-database-master-key.md)   
 [备份数据库主密钥](back-up-a-database-master-key.md)   
 [还原数据库主密钥](restore-a-database-master-key.md)   
 [在两个服务器上创建相同的对称密钥](create-identical-symmetric-keys-on-two-servers.md)  
  
  
