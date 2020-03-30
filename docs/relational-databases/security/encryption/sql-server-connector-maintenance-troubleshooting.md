---
title: SQL Server 连接器维护和疑难解答
description: 了解 SQL Server 连接器的维护说明和常见疑难解答步骤。
ms.custom: seo-lt-2019
ms.date: 07/25/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 050b6ba215d9dc4db433ad81dd8fa48bed212803
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "75557922"
---
# <a name="sql-server-connector-maintenance--troubleshooting"></a>SQL Server 连接器维护与故障排除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题提供了有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器的补充信息。 有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器的详细信息，请参阅 [Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41;（使用 Azure 密钥保管库的可扩展密钥管理）](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)、[Setup Steps for Extensible Key Management Using the Azure Key Vault（使用 Azure 密钥保管库的可扩展密钥管理的设置步骤）](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)和 [Use SQL Server Connector with SQL Encryption Features（使用具有 SQL 加密功能的 SQL Server 连接器）](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)。  
  
  
##  <a name="a-maintenance-instructions-for-ssnoversion-connector"></a><a name="AppendixA"></a> A. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器的维护说明  
  
### <a name="key-rollover"></a>密钥滚动更新  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器要求密钥名称只能使用字符“a-z”、“A-Z”、“0-9”和“-”，其长度限制为 26 个字符。   
> Azure 密钥保管库中具有同一密钥名称的不同密钥版本不会使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器。 若要轮换 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 正在使用的 Azure Key Vault 密钥，必须创建一个具有新的密钥名称的新密钥。  
  
 通常，用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密的服务器非对称密钥每隔 1 - 2 年需要重设版本。 请务必注意，尽管密钥保管库允许重设密钥版本，但客户不应使用该功能来实施版本控制。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器无法处理密钥保管库密钥版本的更改。 若要实施密钥版本控制，客户需要在密钥保管库中创建新密钥，然后在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中重新加密数据加密密钥。  
  
 对于 TDE，可按如下所述实现此目的：  
  
-   **在 PowerShell 中：** 在密钥保管库中创建一个新的非对称密钥（使用与当前的 TDE 非对称密钥不同的名称）。  
  
    ```powershell  
    Add-AzKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
-   **使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 或 sqlcmd.exe：** 使用如第 3 部分的步骤 3 中所示的以下语句。  
  
     导入新的非对称密钥。  
  
    ```sql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]   
    FROM PROVIDER [EKM]   
    WITH PROVIDER_KEY_NAME = 'Key2',   
    CREATION_DISPOSITION = OPEN_EXISTING   
    GO  
    ```  
  
     创建要与新的非对称密钥关联的新登录名（如 TDE 说明中所示）。  
  
    ```sql  
    USE master  
    CREATE LOGIN TDE_Login2   
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     创建要映射到登录名的新凭据。  
  
    ```sql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',   
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789='   
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     选择你要重新加密其数据库加密密钥的数据库。  
  
    ```sql  
    USE [database]  
    GO  
    ```  
  
     重新加密数据库加密密钥。  
  
    ```sql  
    ALTER DATABASE ENCRYPTION KEY   
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-ssnoversion-connector"></a>升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器  

已替换版本 1.0.0.440 和更早的版本，且生产环境不再支持这些版本。 生产环境中支持版本 1.0.1.0 和更高版本。 使用以下说明升级到 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=45344)提供的最新版本。

如果当前在使用版本 1.0.1.0 或更高版本，请按照以下步骤更新到最新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器。 这些说明无需重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。
 
1. 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Microsoft 下载中心 [安装最新版本的](https://www.microsoft.com/download/details.aspx?id=45344)连接器。 在安装程序向导中，将新 DLL 文件保存在与原始 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器 DLL 文件路径不同的文件路径下。 例如，新文件路径可以是： `C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll`
 
2. 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的实例中，运行以下 Transact-SQL 命令，以将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例指向新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器：

    ``` 
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll'
    GO  
    ```

如果当前在使用版本 1.0.0.440 或更低版本，请按照以下步骤更新到最新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器。
  
1.  停止 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例。  
  
2.  停止 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器服务。  
  
3.  使用 Windows 的“程序和功能”功能卸载 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器。  
  
     （或者，你可以重命名 DLL 文件所在的文件夹。 该文件夹的默认名称是“[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for Microsoft Azure Key Vault”。  
  
4.  从 Microsoft 下载中心安装最新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器。  
  
5.  重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例。  
  
6.  运行以下语句来更改 EKM 提供程序，以便开始使用最新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器。 请确保文件路径指向你所下载的最新版本的位置。 （如果新版本将安装在与初始版本相同的位置，则可跳过此步骤。） 
  
    ```sql  
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
7.  请检查使用 TDE 的数据库是否可访问。  
  
8.  在验证更新是否有效之后，可以删除旧 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器文件夹（如果在步骤 3 中你选择将其重命名而不是卸载。）  
  
### <a name="rolling-the-ssnoversion-service-principal"></a>滚动更新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务主体  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 Azure Active Directory 中创建的服务主体作为凭据来访问密钥保管库。  服务主体具有客户端 ID 和身份验证密钥。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 凭据是使用 **VaultName**、 **客户端 ID**和 **身份验证密钥**设置的。  身份验证密钥  在特定的期限内有效（一年或两年）。   在该期限已过之前，必须在 Azure AD 中为服务主体生成新密钥。  然后，必须在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中更改凭据。    [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 为当前会话中的凭据保留缓存，因此，如果凭据发生更改，应重新启动 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 。  
  
### <a name="key-backup-and-recovery"></a>密钥备份和恢复  
应定期备份密钥保管库。 如果保管库中的非对称密钥丢失，可以从备份还原它。 必须使用和以前相同的名称还原密钥，还原 PowerShell 命令将执行此操作（如下面步骤所示）。  
如果保管库丢失，则你需要重新创建一个保管库，并使用以前相同的名称将非对称密钥还原到保管库中。 保管库名称可以不同（也可与以前相同）。 你还必须设置对新保管库的访问权限，以授予 SQL Server 服务主体对 SQL Server 加密方案的所需访问权限，然后调整 SQL Server 凭据以反映新的保管库名称。

概括而言，步骤如下：  
  
* 备份保管库密钥（使用 Backup-AzureKeyVaultKey Powershell cmdlet）。  
* 如果保管库出错，则在同一地理区域*中创建新的保管库。 创建此保管库的用户应在为 SQL Server 设置的服务主体所在的同一默认目录中。  
* 将密钥还原到新保管库（使用 Restore-AzureKeyVaultKey Powershell cmdlet - 这将使用和以前相同的名称还原密钥）。 如果已经存在具有相同名称的密钥，则还原将失败。  
* 向 SQL Server 服务主体授予权限以使用此新的保管库。  
* 修改数据库引擎使用的 SQL Server 凭据以反映新的保管库名称（如果需要）。  
  
只要密钥备份保留在同一个地理区域或国家云，就可以跨 Azure 区域还原密钥备份，这些国家/地区包括：美国、加拿大、日本、澳大利亚、印度、APAC、欧洲、巴西、中国、美国政府或德国。  
  
  
##  <a name="b-frequently-asked-questions"></a><a name="AppendixB"></a> B. 常见问题  
### <a name="on-azure-key-vault"></a>在 Azure 密钥保管库  
  
**密钥操作如何与 Azure 密钥保管库配合使用？**  
 密钥保管库中的非对称密钥用于保护 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密密钥。 仅非对称密钥的公共部分会离开保管库，其私有部分绝不会由保管库导出。 使用非对称密钥的所有加密操作都委托给了 Azure Key Vault 服务，并受到该服务的安全性的保护。  
  
 **什么是密钥 URI？**  
 Azure 密钥保管库中的所有密钥都有一个统一资源标识符 (URI)，你可以使用它在应用程序中引用密钥。 使用格式 `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` 可获取当前版本，使用 `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` 可获取特定的版本。  
  
### <a name="on-configuring-ssnoversion"></a>有关配置 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

SQL Server 连接器需要哪些终结点的访问权限？  该连接器与两个终结点通信，这两个终结点需要列入允许列表。 与这些其他服务进行出站通信所需的唯一端口是 443（用于 Https）：
-  login.microsoftonline.com/*:443
-  *.vault.azure.net/* :443

**如何通过 HTTP(S) 代理服务器连接到 Azure Key Vault？**
连接器使用 Internet Explorer 的代理配置设置。 这些设置可通过[组策略](https://blogs.msdn.microsoft.com/askie/2015/10/12/how-to-configure-proxy-settings-for-ie10-and-ie11-as-iem-is-not-available/)或注册表控制，但需要注意的是，这些设置不是系统范围的设置，而是针对运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的服务帐户。 如果数据库管理员在 Internet Explorer 中查看或编辑设置，则它们只会影响数据管理员的帐户，而不会影响 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 引擎。 不建议使用服务帐户以交互的方式登录到服务器，并且在许多安全环境中都会阻止该方式。 对配置的代理设置进行更改可能需要重启 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例才能生效，因为当连接器首次尝试连接到 Key Vault 时，将缓存这些设置。

**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中每个配置步骤所需的最低权限级别是什么？**  
 尽管你可以使用 sysadmin 固定服务器角色成员的身份执行所有配置步骤，但 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建议你尽量使用最少的权限。 以下列表定义了每个操作的最小权限级别。  
  
-   若要创建加密提供程序，需要具备 `CONTROL SERVER` 权限或 **sysadmin** 固定服务器角色的成员身份。  
  
-   若要更改配置选项并运行 `RECONFIGURE` 语句，你必须具有 `ALTER SETTINGS` 服务器级别权限。 `ALTER SETTINGS` 权限由 sysadmin 和 **serveradmin** 固定服务器角色隐式持有。  
  
-   若要创建凭据，需要具备 `ALTER ANY CREDENTIAL` 权限。  
  
-   若要向登录名添加凭据，需要具备 `ALTER ANY LOGIN` 权限。  
  
-   若要创建非对称密钥，需要具备 `CREATE ASYMMETRIC KEY` 权限。  

**如何更改我的默认 Active Directory，以便在与为 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 连接器创建的服务主体相同的订阅和 Active Directory 中创建我的密钥保管库？**

![aad-change-default-directory-helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. 转到 Azure 经典门户：[https://manage.windowsazure.com](https://manage.windowsazure.com)  
2. 在左侧菜单上，向下滚动并选择“设置”  。
3. 选择当前所使用的 Azure 订阅，然后在屏幕底部的命令中单击“编辑目录”  。
4. 在弹出窗口中，使用“目录”  下拉列表选择要使用的 Active Directory。 这会使它成为默认目录。
5. 请确保你是新选择的 Active Directory 的全局管理员。 如果你不是全局管理员，则可能会由于切换目录而失去管理权限。
6. 弹出窗口关闭之后，如果你看不到你的任何订阅，则可能需要在屏幕右上角菜单的“订阅”  筛选器中更新“按目录筛选”  筛选器，才能看到使用最近更新的 Active Directory 的订阅。

    > [!NOTE] 
    > 你可能没有对 Azure 订阅实际更改默认目录的权限。 在这种情况下，请在默认目录中创建 AAD 服务主体，以便它处于与以后使用的 Azure 密钥保管库相同的目录中。

若要了解有关 Active Directory 的详细信息，请阅读 [Azure 订阅如何与 Azure Active Directory 相关](https://azure.microsoft.com/documentation/articles/active-directory-how-subscriptions-associated-directory/)
  
##  <a name="c-error-code-explanations-for-ssnoversion-connector"></a><a name="AppendixC"></a> C. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接器的错误代码说明  
 **提供程序错误代码：**  
  
错误代码  |符号  |说明    
---------|---------|---------  
0 | scp_err_Success | 操作已成功执行。    
1 | scp_err_Failure | 操作失败。    
2 | scp_err_InsufficientBuffer | 该错误通知引擎为缓冲区分配更多内存。    
3 | scp_err_NotSupported | 此操作不受支持。 例如，EKM 提供程序不支持指定的密钥类型或算法。    
4 | scp_err_NotFound | EKM 提供程序找不到指定的密钥或算法。    
5 | scp_err_AuthFailure | EKM 提供程序的身份验证失败。    
6 | scp_err_InvalidArgument | 提供的参数无效。    
7 | scp_err_ProviderError | EKM 提供程序中发生了 SQL 引擎捕获到的未知错误。   
401 | acquireToken | 服务器已针对请求响应代码 401。 请确保客户端 ID 和密码正确，并凭据字符串是 AAD 客户端 ID 和密码的串联（无连字符）。
404 | getKeyByName | 服务器响应 404，因为找不到密钥名称。 请确保保管库中存在密钥名称。
2049 | scp_err_KeyNameDoesNotFitThumbprint | 密钥名称太长，不适用于 SQL 引擎的指纹。 密钥名称不得超过 26 个字符。    
2050 | scp_err_PasswordTooShort | 作为 AAD 客户端 ID 和密码的串联的密码字符串少于 32 个字符。    
2051 | scp_err_OutOfMemory | SQL 引擎内存不足，无法为 EKM 提供程序分配内存。    
2052 | scp_err_ConvertKeyNameToThumbprint | 无法将密钥名称转换为指纹。    
2053 | scp_err_ConvertThumbprintToKeyName|  无法将指纹转换为密钥名称。    
3000 | ErrorSuccess | AKV 操作已成功。    
3001 | ErrorUnknown | AKV 操作失败，并出现未知错误。    
3002 | ErrorHttpCreateHttpClientOutOfMemory | 由于内存不足，无法为 AKV 操作创建 HttpClient。    
3003 | ErrorHttpOpenSession | 由于网络错误，无法打开 Http 会话。    
3004 | ErrorHttpConnectSession | 由于网络错误，无法连接 Http 会话。    
3005 | ErrorHttpAttemptConnect | 由于网络错误，无法尝试连接。    
3006 | ErrorHttpOpenRequest | 由于网络错误，无法打开请求。    
3007 | ErrorHttpAddRequestHeader | 无法添加请求标头。    
3008 | ErrorHttpSendRequest | 由于网络错误，无法发送请求。    
3009 | ErrorHttpGetResponseCode | 由于网络错误，无法获取响应代码。    
3010 | ErrorHttpResponseCodeUnauthorized | 服务器已针对请求响应代码 401。    
3011 | ErrorHttpResponseCodeThrottled | 服务器已限制请求。    
3012 | ErrorHttpResponseCodeClientError | 从连接器发送的请求无效。 这通常意味着密钥名称无效或包含无效字符。
3013 | ErrorHttpResponseCodeServerError | 服务器响应的响应代码介于 500 和 600 之间。    
3014 | ErrorHttpQueryHeader | 无法查询响应标头。    
3015 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader | 由于内存不足，无法复制响应标头。    
3016 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer | 重新分配缓冲区时，由于内存不足无法查询响应标头。    
3017 | ErrorHttpQueryHeaderNotFound | 在响应中找不到查询标头。    
3018 | ErrorHttpQueryHeaderUpdateBufferLength | 查询响应标头时无法更新缓冲区长度。    
3019 | ErrorHttpReadData | 由于网络错误，无法读取响应数据。 
3076 | ErrorHttpResourceNotFound | 服务器响应 404，因为找不到密钥名称。 确保保管库中存在密钥名称。
3077 | ErrorHttpOperationForbidden | 服务器响应 403，因为用户没有执行操作的正确权限。 确保你具有用于指定操作的权限。 连接器至少需要“get、list、wrapKey、unwrapKey”权限才能正常运行。   
  
如果未在此表中看到你的错误代码，以下是发生此错误的一些其他原因：   
  
-   你可能无法访问 Internet，以及无法访问 Azure Key Vault - 请检查你的 Internet 连接。  
  
-   Azure 密钥保管库服务可能已关闭。 另选时间重试一次。  
  
-   你可能已从 Azure 密钥保管库或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中删除非对称密钥。 还原此密钥。  
  
-   如果你收到“无法加载库”的错误消息，请确保已安装适当版本的 Visual Studio C++ 可再发行组件，该组件版本基于当前运行的 SQL Server 版本。 下表指定了应从 Microsoft 下载中心安装的版本。   

Windows 事件日志还会记录与 SQL Server 连接器相关的错误，这有助于了解为何其他上下文也会出现这些错误。 Windows 应用程序事件日志中的源将为“用于 Microsoft Azure Key Vault 的 SQL Server 连接器”。
  
SQL Server 版本  |可再发行组件安装链接    
---------|--------- 
2008、2008 R2、2012、2014 | [适用于 Visual Studio 2013 的 Visual C++ 可再发行组件包](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
  
  
## <a name="additional-references"></a>其他参考  
 有关可扩展密钥管理的更多信息：  
  
-   [可扩展密钥管理 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 支持 EKM 的 SQL 加密：  
  
-   [使用 EKM 在 SQL Server 上启用 TDE](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
-   [备份加密](../../../relational-databases/backup-restore/backup-encryption.md)  
  
-   [创建加密的备份](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 相关 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令：  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Azure 密钥保管库文档：  
  
-   [什么是 Azure 密钥保管库？](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)  
  
-   [Azure Key Vault 入门](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)  
  
-   PowerShell [Azure 密钥保管库 Cmdlet](/powershell/module/azurerm.keyvault/) 参考  
  
## <a name="see-also"></a>另请参阅

 [使用 Azure Key Vault 的可扩展密钥管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [使用具有 SQL 加密功能的 SQL Server 连接器](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)  
 [EKM provider enabled 服务器配置选项](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
 [Setup Steps for Extensible Key Management Using the Azure Key Vault（使用 Azure 密钥保管库的可扩展密钥管理的设置步骤）](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)
