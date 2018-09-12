---
title: 使用 Azure Key Vault 的 SQL Server TDE 可扩展密钥管理 - 安装步骤 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
caps.latest.revision: 34
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 4f8581201f9303c87a848a7456849efa7a09396a
ms.sourcegitcommit: 0ab652fd02039a014c9661f3c5ccf4281cfb025b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2018
ms.locfileid: "42925987"
---
# <a name="sql-server-tde-extensible-key-management-using-azure-key-vault---setup-steps"></a>使用 Azure Key Vault 的 SQL Server TDE 可扩展密钥管理 - 安装步骤
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  以下步骤演示了如何安装和配置 Azure Key Vault 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器。  
  
## <a name="before-you-start"></a>开始之前  
 要将 Azure 密钥保管库用于 SQL Server，有几个先决条件：  
  
-   必须具有 Azure 订阅  
  
-   安装最新的 [Azure PowerShell](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/)（5.2.0 或更高版本）。  

-   创建 Azure Active Directory  

-   通过查阅[Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41;（使用 Azure 密钥保管库的可扩展密钥管理）](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)熟悉使用 Azure 密钥保管库的 EKM 存储的主体。  

-   已安装适当版本的 Visual Studio C++ 可再发行组件，该组件版本基于当前运行的 SQL Server 版本：
  
SQL Server 版本  |可再发行组件安装链接    
---------|--------- 
2008、2008 R2、2012、2014 | [适用于 Visual Studio 2013 的 Visual C++ 可再发行组件包](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [适用于 Visual Studio 2015 的 Visual C++ 可再发行组件](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="part-i-set-up-an-azure-active-directory-service-principal"></a>第 I 部分：设置 Azure Active Directory 服务主体  
 为了向 Azure 密钥保管库授予 SQL Server 访问权限，你需要在 Azure Active Directory (AAD) 中具有服务主体帐户。  
  
1.  转到 [Azure 门户](https://ms.portal.azure.com/)，并登录。  
  
2.  在 Azure Active Directory 中注册应用程序。 有关注册应用程序的详细步骤说明，请参阅 **Azure 密钥保管库博客** 中的 [获取应用程序的标识](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)部分。  
  
3.  复制 **客户端 ID** 和 **客户端密码** 用于后续步骤，即用于向密钥保管库授予 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 访问权限。  
  
 ![ekm-client-id](../../../relational-databases/security/encryption/media/ekm-client-id.png "ekm-client-id")  
  
 ![ekm-key-id](../../../relational-databases/security/encryption/media/ekm-key-id.png "ekm-key-id")  
  
## <a name="part-ii-create-a-key-vault-and-key"></a>第 II 部分：创建密钥保管库和密钥  
 此处创建的密钥保管库和密钥将供 SQL Server 数据库引擎使用，以实现加密密钥保护。  
  
> [!IMPORTANT]  
>  在其中创建密钥保管库的订阅必须与创建 Azure Active Directory 服务主体位于同一默认的 Azure Active Directory 中。 如果想要使用默认 Active Directory 以外的 Active Directory 来创建 SQL Server 连接器的服务主体，必须在创建密钥保管库前先更改 Azure 帐户中的默认 Active Directory。 若要了解如何将默认 Active Directory 更改为希望使用的 Active Directory，请参考 SQL Server 连接器 [常见问题解答](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)。  
  
1.  **打开 PowerShell 并登录**  
  
     安装并启动最新的 [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)（5.2.0 或更高版本）。 使用以下命令登录到你的 Azure 帐户：  
  
    ```powershell  
    Login-AzureRmAccount  
    ```  
  
     该语句返回：  
  
    ```  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    >  如果你有多个订阅并想要指定其中一个用于保管库，请使用 `Get-AzureRmSubscription` 查看订阅，然后使用 `Select-AzureRmSubscription` 选择适当的订阅。 否则，PowerShell 将默认为你选择一个订阅。  
  
2.  **创建新资源组**  
  
     资源组中必须包含通过 Azure 资源管理器创建的所有 Azure 资源。 创建资源组用于包含密钥保管库。 此示例使用 `ContosoDevRG`。 选择你自己的 **唯一** 资源组和密钥保管库名称，因为所有密钥保管库名称是全局唯一的。  
  
    ```powershell  
    New-AzureRmResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
     该语句返回：  
  
    ```  
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :   
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]  
    >  对于 `-Location parameter`参数，请使用命令 `Get-AzureLocation` 来确定如何将备用位置指定为本示例中的位置之一。 如需详细信息，请键入： `Get-Help Get-AzureLocation`  
  
3.  **创建密钥保管库**  
  
     `New-AzureRmKeyVault` cmdlet 需要一个资源组名称、一个密钥保管库名称和一个地理位置。 例如，对于名为 `ContosoDevKeyVault`的密钥保管库，请键入：  
  
    ```powershell  
    New-AzureRmKeyVault -VaultName 'ContosoDevKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
     记录密钥保管库的名称。  
  
     该语句返回：  
  
    ```  
    Vault Name                       : ContosoDevKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoDevKeyVault  
    Vault URI: https://ContosoDevKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :   
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,   
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
4.  **为 Azure Active Directory 服务主体授予权限以访问密钥保管库**  
  
     你可以授权其他用户和应用程序使用密钥保管库。   
    在本例中，让我们使用在第 I 部分中创建的 Azure Active Directory 服务主体来授权 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。  
  
    > [!IMPORTANT]  
    >  Azure Active Directory 服务主体必须至少具有密钥保管库的 `get`、 `wrapKey` 和 `unwrapKey` 权限。  
  
     如下所示，对 **参数使用第 I 部分的** 客户端 ID `ServicePrincipalName` 。 如果 `Set-AzureRmKeyVaultAccessPolicy` 成功运行，则以无提示方式运行，并且无任何输出。  
  
    ```powershell  
    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoDevKeyVault'`  
      -ServicePrincipalName EF5C8E09-4D2A-4A76-9998-D93440D8115D `  
      -PermissionsToKeys get, wrapKey, unwrapKey  
    ```  
  
     调用 `Get-AzureRmKeyVault` cmdlet 以确认权限。 在“访问策略”下方的语句输出中，你应看到作为有权访问此密钥保管库的另一个租户列出的 AAD 应用程序名称。  
  
       
5.  **在密钥保管库中生成非对称密钥**  
  
     在 Azure 密钥保管库中生成密钥有两种方法：1) 导入现有的密钥或 2) 创建新的密钥。  
                  
      > [!NOTE]
        >  SQL Server 仅支持 2048 位 RSA 密钥。
        
    ### <a name="best-practice"></a>最佳做法：
    
    为了确保快速恢复密钥并能够访问 Azure 外的数据，建议采用以下最佳做法：
 
    1. 在本地 HSM 设备上以本地方式创建加密密钥。 （确保此密钥是一个非对称的 RSA 2048 密钥，以便受 SQL Server 支持。）
    2. 将加密密钥导入到 Azure 密钥保管库。 请参阅以下步骤了解如何执行此操作。
    3. 在首次使用 Azure 密钥保管库中的密钥之前，先进行 Azure 密钥保管库密钥备份。 了解有关 [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) 命令的详细信息。
    4. 每次更改密钥（例如添加 ACL、添加标记、添加键属性）时，务必再进行一次 Azure Key Vault 密钥备份。

        > [!NOTE]  
        >  备份密钥是一项 Azure Key Vault 密钥操作，将返回一个可在任意位置保存的文件。

    ### <a name="types-of-keys"></a>密钥类型：
    在 Azure Key Vault 中可以生成将用于 SQL Server 的两种类型的密钥。 这两种密钥都是非对称 2048 位 RSA 密钥。  
  
    -   **受软件保护的密钥：** 在软件中处理，在静止时加密。 在 Azure 虚拟机上执行对受软件保护的密钥的操作。 建议用于不在生产部署中使用的密钥。  
  
    -   **受 HSM 保护的密钥：** 由硬件安全模块 (HSM) 创建并保护，以增加安全性。 每个密钥版本的费用大约为 1 美元。  
  
        > [!IMPORTANT]  
        >  SQL Server 连接器要求密钥名称只能使用字符“a-z”、“A-Z”、“0-9”和“-”，其长度限制为 26 个字符。   
        > Azure 密钥保管库中具有同一密钥名称的不同密钥版本不会使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器。 若要轮换 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用的 Azure 密钥保管库密钥，请参阅 [SQL Server 连接器维护与故障排除](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)熟悉使用 Azure 密钥保管库的 EKM 存储的主体。  

    ### <a name="import-an-existing-key"></a>导入现有密钥   
  
    如果已有 2048 位 RSA 软件保护密钥，则可以将该密钥上传到 Azure 密钥保管库。 例如，如果 `C:\\` 驱动器中保存了要上传到 Azure 密钥保管库的、名为 `softkey.pfx` 的 .PFX 文件，请键入以下内容，以便为该 .PFX 文件的密码 `securepfxpwd` 设置变量 `12987553` ：  
  
    ``` powershell  
    $securepfxpwd = ConvertTo-SecureString –String '12987553' `  
      –AsPlainText –Force  
    ```  
  
    然后可以键入以下内容从 .PFX 文件导入密钥，以便硬件（建议）在密钥保管库服务中保护密钥：  
  
    ``` powershell  
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
          -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
          -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
    ```  
 
    > [!IMPORTANT]  
    > 强烈建议对生产情况导入非对称密钥，因为这样管理员就可以在密钥托管系统中托管密钥。 如果非对称密钥是在保管库中创建的，则无法托管，因为私有密钥无法离开保管库。 应托管用于保护关键数据的密钥。 丢失非对称密钥将导致永久性数据丢失。  

    ### <a name="create-a-new-key"></a>创建新密钥
    #### <a name="example"></a>例如：  
    或者，可直接在 Azure Key Vault 中创建新的加密密钥，并使其受软件保护或受 HSM 保护。  在此示例中，让我们使用 `Add-AzureKeyVaultKey cmdlet`创建软件保护的密钥：  

    ``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'ContosoRSAKey0' -Destination 'Software'  
    ```  
  
    该语句返回：  
  
    ```  
    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
    Key        :  {"kid":"https:contosodevKeyVault.azure.net/keys/  
                   ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
    VaultName  : contosodevkeyvault  
    Name       : contosoRSAKey0  
    Version    : <guid>  
    Id         : https://contosodevkeyvault.vault.azure.net:443/  
                 keys/ContosoRSAKey0/<guid>  
    ```  
 > [!IMPORTANT]  
    >  虽然密钥保管库支持具有多个版本的相同命名的密钥，但 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器使用的密钥不应受版本控制或对其进行滚动更新。 如果管理员想要滚动用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密的密钥，则应在保管库中创建一个具有不同名称的新密钥并用它来加密 DEK。  
   
  
## <a name="part-iii-install-the-includessnoversionincludesssnoversion-mdmd-connector"></a>第 III 部分：安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器  
 从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/p/?LinkId=521700)下载 SQL Server 连接器。 （此操作应由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 计算机的管理员完成。）  

> [!NOTE]  
>  已替换版本 1.0.0.440 和更早的版本，且生产环境不再支持这些版本。 要升级至版本 1.0.1.0 或更高版本，请访问 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=45344) ，并参照“升级 SQL Server 连接器”下 [SQL Server 连接器维护与故障排除](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) 页面上的指南。
  
 ![ekm-connector-install](../../../relational-databases/security/encryption/media/ekm-connector-install.png "ekm-connector-install")  
  
 默认情况下，连接器安装在 C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault 中。 可在设置过程中更改此位置。 （若已更改，请调整以下脚本。）  
  
 该连接器没有接口，但如果安装成功，将在计算机上安装 **Microsoft.AzureKeyVaultService.EKM.dll** 这是加密 EKM 提供程序 DLL，需要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语句在 `CREATE CRYPTOGRAPHIC PROVIDER` 中注册。  
  
 SQL Server 连接器安装还允许你选择性地下载用于 SQL Server 加密的示例脚本。  
  
 若要查看 SQL Server 连接器的错误代码说明、配置设置或维护任务，请访问本主题底部的附录：  
  
-   [A.SQL Server 连接器的维护说明](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
  
-   [C.SQL Server 连接器的错误代码说明](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="part-iv-configure-includessnoversionincludesssnoversion-mdmd"></a>第 IV 部分：配置 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 请参阅 [B. 常见问题解答](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)以查看本节中每个操作所需的最低权限级别的说明。  
  
1.  **启动 sqlcmd.exe 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio。**  
  
2.  **配置 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以使用 EKM**  
  
     执行以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 脚本配置 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 以使用 EKM 提供程序。  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
3.  **将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器注册（创建）为 EKM 提供程序 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     -- 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器（Azure Key Vault 的 EKM 提供程序）创建加密提供程序。    
    此示例使用名称 `AzureKeyVault_EKM_Prov`。  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
    > [!NOTE]  
    >  文件路径长度不能超过 256 个字符。  
  
  
4.  **为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名设置 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 凭据以使用密钥保管库**  
  
     必须将凭据添加到要使用密钥保管库中密钥执行加密的每个登录名。 这些登录名可能包括：  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理员登录名，要使用密钥保管库以便设置并管理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密方案。  
  
    -   其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名，已启用透明数据加密 (TDE) 或其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密功能。  
  
     凭据和登录名之间是一对一的映射关系。 也就是说，每个登录名必须具有唯一的凭据。  
  
     采用以下方式修改下面的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 脚本：  
  
    -   编辑 `IDENTITY` 参数 (`ContosoDevKeyVault`) 以指向 Azure 密钥保管库。
        - 如果使用“全局 Azure”，请将 `IDENTITY` 参数替换为第 II 部分中的 Azure Key Vault 的名称。
        - 如果使用 **Azure 私有云** （例如， Azure 政府、Azure 中国或 Azure 德国），请将 `IDENTITY` 参数替换为第 II 部分的步骤 3 中返回的保管库 URI。 保管库 URI 中不能包含 “https://”。   
    -   将 `SECRET` 参数的第一部分替换为第 I 部分中的 Azure Active Directory **客户端 ID** 。在此示例中， **客户端 ID** 为 `EF5C8E094D2A4A769998D93440D8115D`。  
  
        > [!IMPORTANT]  
        >  必须删除 **客户端 ID**中的连字符。  
  
    -   使用第 I 部分的 `SECRET` 客户端密码 **完成** 参数的第二部分。在此示例中，第 I 部分的 **客户端密码** 为 `Replace-With-AAD-Client-Secret`。 `SECRET` 参数的最终字符串是一长串 *不带连字符*的字母和数字。  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     有关使用 **CREATE CREDENTIAL** 参数的变量和以编程方式从客户端 ID 中删除连字符的示例，请参阅[创建凭据 &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)。  
  
5.  **打开 Azure 密钥保管库密钥 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     如果按照上述第 II 部分所述导入了一个非对称密钥，请通过在以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 脚本中提供密钥名称来打开密钥。  
  
    -   将 `CONTOSO_KEY` 替换为你想要的该密钥在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的名称。  
  
    -   将 `ContosoRSAKey0` 替换为 Azure 密钥保管库中的密钥的名称。  
  
    ```sql  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
## <a name="next-step"></a>下一步  
  
现在你已完成基本配置，请参阅如何 [使用具有 SQL 加密功能的 SQL Server 连接器](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)   
  
## <a name="see-also"></a>另请参阅  
 [使用 Azure Key Vault 的可扩展密钥管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
[SQL Server 连接器维护与故障排除](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
