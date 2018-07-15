---
title: 使用 Azure Key Vault 的可扩展密钥管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault
- TDE, EKM and key vault
- Extensible Key Management with key vault
- Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
caps.latest.revision: 37
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: ecd049528577ff5da601bf37fda3e8b356acb0e3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37305427"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>使用 Azure Key Vault 的可扩展密钥管理 (SQL Server)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用于连接器[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Azure 密钥保管库启用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密，以将 Azure 密钥保管库服务用作[可扩展密钥管理&#40;EKM&#41; ](extensible-key-management-ekm.md)提供程序以保护其加密密钥。  
  
 本主题内容：  
  
-   [使用 EKM](#Uses)  
  
-   [步骤 1： 设置密钥保管库用于 SQL Server](#Step1)  
  
-   [步骤 2： 安装 SQL Server 连接器](#Step2)  
  
-   [步骤 3： 配置 SQL Server 以使用 EKM 提供程序用于 Key Vault](#Step3)  
  
-   [通过使用密钥保管库的非对称密钥的示例 a： 透明数据加密](#ExampleA)  
  
-   [示例 b： 通过使用密钥保管库的非对称密钥加密备份](#ExampleB)  
  
-   [通过使用密钥保管库的非对称密钥的示例 c： 列级加密](#ExampleC)  
  
##  <a name="Uses"></a> 使用 EKM  
 组织可使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密来保护敏感数据。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密包括[透明数据加密&#40;TDE&#41;](transparent-data-encryption.md)，[列级加密](/sql/t-sql/functions/cryptographic-functions-transact-sql)(CLE) 和[备份加密](../../backup-restore/backup-encryption.md)。 在这几种情况下，均使用对称数据加密密钥对数据进行加密。 通过使用存储在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的密钥层次结构对对称数据加密密钥进行加密而使其获得进一步的保护。 或者，EKM 提供程序体系结构使[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用外部存储的非对称密钥保护数据加密密钥[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部加密提供程序中。 使用 EKM 提供程序体系结构会额外提供一层安全保护，使组织可分开管理密钥和数据。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure 密钥保管库的连接器可让[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可以可缩放、 高性能和高度可用的密钥保管库服务用作 EKM 提供程序实现加密密钥保护。 密钥保管库服务可与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上的安装[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Azure 虚拟机以及在本地服务器。 Key Vault 服务还提供一种选择，即使用受到严格控制和监视的硬件安全模块 (HSM) 来实现对非对称加密密钥的更高级别的保护。 有关密钥保管库的详细信息，请参阅 [Azure 密钥保管库](http://go.microsoft.com/fwlink/?LinkId=521401)。  
  
 下图总结了使用密钥保管库的 EKM 处理流程。 图中的处理步骤数与以下的设置步骤数并不一致。  
  
 ![使用 Azure Key Vault 的 SQL Server EKM](../../../database-engine/media/ekm-using-azure-key-vault.png "使用 Azure Key Vault 的 SQL Server EKM")  
  
##  <a name="Step1"></a> 步骤 1： 设置密钥保管库用于 SQL Server  
 使用以下步骤设置 Key Vault，使其可与 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 一起使用来实现对加密密钥的保护。 组织可能已使用了某个保管库。 保管库不存在，当您指定管理加密密钥的组织中的 Azure 管理员可以创建保管库，在保管库中生成非对称密钥，然后授权[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用该密钥。 请查看 [Azure Key Vault 入门](http://go.microsoft.com/fwlink/?LinkId=521402)和 PowerShell [Azure Key Vault Cmdlet](http://go.microsoft.com/fwlink/?LinkId=521403) 参考，详细了解 Key Vault 服务的相关内容。  
  
> [!IMPORTANT]  
>  如果有多个 Azure 订阅，则必须使用包含的订阅[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
1.  **创建保管库：** 请使用 **Azure 密钥保管库入门** 中的 [创建密钥保管库](http://go.microsoft.com/fwlink/?LinkId=521402)部分中的说明来创建保管库。 记录保管库的名称。 本主题将 **ContosoKeyVault** 作为 Key Vault 名称。  
  
2.  **在保管库中生成非对称密钥：** 密钥保管库中的非对称密钥用于保护[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密密钥。 仅非对称密钥的公共部分会离开保管库，其私有部分绝不会由保管库导出。 使用非对称密钥的所有加密操作都委托给了 Azure Key Vault，并受到 Key Vault 安全性的保护。  
  
     你可通过若干方法生成不对称密钥并将其存储在保管库中。 你可在外部生成密钥，然后将其作为 .pfx 文件导入保管库。 或者使用密钥保管库 API 直接在保管库中创建密钥。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]连接器要求非对称密钥为 2048年位 RSA 和密钥名称只能使用字符"a-z"、"A-Z"、"0-9"、 和"-"。 在本文档中，非对称密钥名称被称为 **ContosoMasterKey**。 将名称替换为你用于密钥的唯一名称。  
  
    > [!IMPORTANT]  
    >  强烈建议对生产情况导入非对称密钥，因为这样管理员就可以在密钥托管系统中托管密钥。 如果非对称密钥是在保管库中创建的，则无法托管，因为私有密钥无法离开保管库。 应托管用于保护关键数据的密钥。 丢失非对称密钥将导致数据永久性不可恢复。  
  
    > [!IMPORTANT]  
    >  Key Vault 支持多个版本的具有相同命名的密钥。 若要使用的密钥[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]连接器不应受版本控制或回滚。 如果管理员想要滚动用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密的密钥，则应在保管库中创建一个具有不同名称的新密钥并用它来加密 DEK。  
  
     有关如何导入密钥保管库或 （不建议用于生产环境） 在 key vault 中创建密钥的详细信息，请参阅**将密钥或机密添加到密钥保管库**主题中[开始使用 Azure密钥保管库](http://go.microsoft.com/fwlink/?LinkId=521402)。  
  
3.  **获取 Azure Active Directory 服务主体以用于 SQL Server：** 当组织注册 Microsoft 云服务时，即获取 Azure Active Directory。 创建**服务主体**有关 Azure Active Directory 中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]时要使用 （若要向 Azure Active Directory 验证自身身份） 访问密钥保管库。  
  
    -   一个**服务主体**将所需的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理员才能配置时访问保管库[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用加密。  
  
    -   另一个**服务主体**将所需的[!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]解包中使用的密钥保管库的访问[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密。  
  
     有关如何注册应用程序和生成服务主体的详细信息，请参阅 **Azure Key Vault 入门** 中的 [向 Azure Active Directory 注册应用程序](http://go.microsoft.com/fwlink/?LinkId=521402)部分。 注册过程将针对每一个 Azure Active Directory **服务主体** 返回一个 **应用程序 ID**（也称为 **客户端 ID** ）和一个 **身份验证密钥**（也称为 **Secret**）。 在中使用时`CREATE CREDENTIAL`语句，必须从删除连字符**客户端 ID**。 记录这些密钥，以在下面的脚本中使用：  
  
    -    登录的 **服务主体** ： **CLIENTID_服务主体_login** 和 **SECRET_服务主体_login**  
  
    -   **服务主体**有关[!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine**并**SECRET_DBEngine**。  
  
4.  **授予服务主体访问密钥保管库的权限：** 和 **和**  **服务主体** 均需要密钥保管库中的 **get**, **list**, **wrapKey**,  **unwrapKey** 权限。 如果你想要创建通过密钥[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]还需要授予**创建**密钥保管库中的权限。  
  
    > [!IMPORTANT]  
    >  用户至少必须拥有用于 Key Vault 的 **wrapKey** 和 **unwrapKey** 操作。  
  
     有关授予对保管库的权限的详细内容，请参阅 **Azure Key Vault 入门**[中的授权应用程序使用密钥或机密](http://go.microsoft.com/fwlink/?LinkId=521402)部分。  
  
     链接至 Azure Key Vault 文档  
  
    -   [什么是 Azure Key Vault？](http://go.microsoft.com/fwlink/?LinkId=521401)  
  
    -   [Azure Key Vault 入门](http://go.microsoft.com/fwlink/?LinkId=521402)  
  
    -   PowerShell [Azure 密钥保管库 Cmdlet](http://go.microsoft.com/fwlink/?LinkId=521403) 参考  
  
##  <a name="Step2"></a> 步骤 2： 安装 SQL Server 连接器  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]下载并安装由管理员连接器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]计算机。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]连接器是可从下载[Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=521700)。  搜索 **适用于 Microsoft Azure Key Vault 的 SQL Server Connector**，查看详细内容、系统要求和安装说明，然后选择下载连接器并使用“运行” 开始进行安装。 查看许可证，接受许可证，然后继续。  
  
 默认情况下，连接器安装在 **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**处。 可在设置过程中更改此位置。 （若已更改，请调整以下脚本。）  
  
 安装完成时，以下内容将安装到计算机：  
  
-   **Microsoft.AzureKeyVaultService.EKM.dll**： 这是加密 EKM 提供程序 DLL，需要使用注册[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]通过使用 CREATE CRYPTOGRAPHIC PROVIDER 语句。  
  
-   **Azure Key Vault SQL Server Connector**：这是一个 Windows 服务，使加密 EKM 提供程序可以与 Key Vault 进行通信。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]连接器安装还允许你选择性地下载的示例脚本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密。  
  
##  <a name="Step3"></a> 步骤 3： 配置 SQL Server 以使用 EKM 提供程序用于 Key Vault  
  
###  <a name="Permissions"></a> Permissions  
 若要完成整个流程，需要具备 CONTROL SERVER 权限或 **sysadmin** 固定服务器角色的成员身份。 特定操作要求具有以下权限：  
  
-   若要创建加密提供程序，需要具备 CONTROL SERVER 权限或 **sysadmin** 固定服务器角色的成员身份。  
  
-   若要更改配置选项以及运行 RECONFIGURE 语句，你必须具有 ALTER SETTINGS 服务器级别权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
-   若要创建凭据，则需要 ALTER ANY CREDENTIAL 权限。  
  
-   若要向登录添加凭据，需要 ALTER ANY LOGIN 权限。  
  
-   若要创建非对称密钥，需要 CREATE ASYMMETRIC KEY 权限。  
  
###  <a name="TsqlProcedure"></a> 若要配置 SQL Server 以使用加密提供程序  
  
1.  配置 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 以使用 EKM，并对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 注册（创建）加密提供程序。  
  
    ```  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
  
    -- Create a cryptographic provider, using the SQL Server Connector  
    -- which is an EKM provider for the Azure Key Vault. This example uses   
    -- the name AzureKeyVault_EKM_Prov.  
  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO   
    ```  
  
2.  安装程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]凭据[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 key vault，以便设置和管理管理员登录名[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密方案。  
  
    > [!IMPORTANT]  
    >  **标识**自变量的`CREATE CREDENTIAL`需要密钥保管库名称。 **机密**的参数`CREATE CREDENTIAL`需要*\<客户端 ID >* （无连字符） 和*\<机密 >* 传递在一起，消除它们之间的空间。  
  
     在下例中， **客户端 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) 去掉了连字符，并输入为字符串 `EF5C8E094D2A4A769998D93440D8115D` ，而 **Secret** 则表示为字符串 *SECRET_sysadmin_login*。  
  
    ```  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
  
    -- Add the credential to the SQL Server administrators domain login   
    ALTER LOGIN [<domain>/<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     有关使用的变量的示例`CREATE CREDENTIAL`自变量和以编程方式删除连字符，从客户端 ID，请参阅[CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)。  
  
3.  如果按照上述章节 3 步骤 1 中所述导入了一个非对称密钥，请通过在下例中提供密钥名称来打开密钥。  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
  
     虽然不建议用于生产（因为无法导出密钥），但还是可以从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 直接在保管库中创建非对称密钥。 如果之前未导入密钥，请使用以下脚本在 key vault 中创建一个用于测试的非对称密钥。 使用 **sysadmin_ekm_cred** 凭据随附的登录来执行脚本。  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH ALGORITHM = RSA_2048,  
    PROVIDER_KEY_NAME = 'ContosoMasterKey';  
    ```  
  
> [!TIP]  
>  用户收到错误**无法从提供程序中导出公钥。提供程序错误代码： 2053年。** 应在密钥保管库中检查它们的 **get**、 **list**、 **wrapKey**、 and **unwrapKey** 权限。  
  
 有关详细信息，请参见以下内容：  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
## <a name="examples"></a>示例  
  
###  <a name="ExampleA"></a> 通过使用密钥保管库的非对称密钥的示例 a： 透明数据加密  
 完成以上步骤后，创建一个凭据和一个登录，然后创建一个受 Key Vault 中非对称密钥保护的数据库加密密钥。 使用数据库加密密钥对带 TDE 的数据库进行加密。  
  
 若要加密数据库，需要对数据库的 CONTROL 权限。  
  
##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>使用 EKM 和 Key Vault 启用 TDE  
  
1.  创建 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 凭据，以供 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 在数据库加载期间访问 key vault EKM 时使用。  
  
    > [!IMPORTANT]  
    >  **标识**自变量的`CREATE CREDENTIAL`需要密钥保管库名称。 **机密**的参数`CREATE CREDENTIAL`需要*\<客户端 ID >* （无连字符） 和*\<机密 >* 传递在一起，消除它们之间的空间。  
  
     在下例中， **客户端 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) 去掉了连字符，并输入为字符串 `EF5C8E094D2A4A769998D93440D8115D` ，而 **Secret** 则表示为字符串 *SECRET_DBEngine*。  
  
    ```  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
    ```  
  
2.  创建一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录以便 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 将其用于 TDE，并对其添加凭据。 此示例使用存储在 key vault 中的 CONTOSO_KEY 非对称密钥，该密钥是之前如上面的 [章节 3 步骤 3](#Step3) 中所述为主数据库导入或创建的。  
  
    ```  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  创建将用于 TDE 的数据库加密密钥 (DEK)。 可使用任何 SQL Server 支持的算法或密钥长度来创建 DEK。 DEK 将受到 key vault 中的非对称密钥保护。  
  
     此示例使用存储在 key vault 中的 CONTOSO_KEY 非对称密钥，该密钥是之前如上面的 [章节 3 步骤 3](#Step3) 中所述导入或创建的。  
  
    ```  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_128   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
     有关详细信息，请参见以下内容：  
  
    -   [CREATE DATABASE ENCRYPTION KEY (Transact-SQL)](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
    -   [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)  
  
###  <a name="ExampleB"></a> 示例 b： 通过使用密钥保管库的非对称密钥加密备份  
 从 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]开始支持加密备份。 以下示例创建并还原了经过数据加密密钥加密的备份文件，其中该加密密钥受到 key vault 中的非加密密钥保护。  
  
```  
USE master;  
BACKUP DATABASE [DATABASE_TO_BACKUP]  
TO DISK = N'[PATH TO BACKUP FILE]'   
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);  
GO  
```  
  
 还原代码示例。  
  
```  
RESTORE DATABASE [DATABASE_TO_BACKUP]  
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;  
GO  
```  
  
 有关备份选项的详细信息，请参阅[备份&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)。  
  
###  <a name="ExampleC"></a> 通过使用密钥保管库的非对称密钥的示例 c： 列级加密  
 以下示例创建了受 key vault 中非对称密钥保护的对称密钥。 然后该对称密钥用于对数据库中的数据进行加密。  
  
 此示例使用存储在 key vault 中的 CONTOSO_KEY 非对称密钥，该密钥是之前如上面的 [章节 3 步骤 3](#Step3) 中所述导入或创建的。 若要在 `ContosoDatabase` 数据库中使用此非对称密钥，必须再次执行 CREATE ASYMMETRIC KEY 语句，为 `ContosoDatabase` 数据库提供对该密钥的引用。  
  
```  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>请参阅  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [可扩展密钥管理 &#40;EKM&#41;](extensible-key-management-ekm.md)   
 [使用 EKM 启用 TDE](enable-tde-on-sql-server-using-ekm.md)   
 [备份加密](../../backup-restore/backup-encryption.md)   
 [创建加密的备份](../../backup-restore/create-an-encrypted-backup.md)  
  
  
