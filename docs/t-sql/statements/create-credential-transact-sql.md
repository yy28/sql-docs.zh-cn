---
title: "创建凭据 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREDENTIAL_TSQL
- SQL13.SWB.CREDENTIAL.GENERAL.F1
- CREATE CREDENTIAL
- CREATE_CREDENTIAL_TSQL
- CREDENTIAL
dev_langs:
- TSQL
helpviewer_keywords:
- SECRET clause
- authentication [SQL Server], credentials
- CREATE CREDENTIAL statement
- credentials [SQL Server], CREATE CREDENTIAL statement
ms.assetid: d5e9ae69-41d9-4e46-b13d-404b88a32d9d
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 556fa0262696075d63ee549730f2d9824c482dd4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建服务器级别凭据。 凭据是包含连接到 SQL Server 以外的资源所需的身份验证信息的记录。 多数凭据包括一个 Windows 用户和一个密码。 例如，将数据库备份保存到某个位置，可能需要提供特殊的凭据来访问该位置的 SQL Server。 有关详细信息，请参阅[凭据 （数据库引擎）](../../relational-databases/security/authentication-access/credentials-database-engine.md)。
  
> [!NOTE]  
>  若要使凭据在数据库级别使用[CREATE DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). 当您需要对服务器上的多个数据库使用相同的凭据时，请使用服务器级别凭据。 使用数据库范围的凭据以使数据库更易于移植。 当数据库移动到新服务器，将随它一起移动的数据库范围凭据。 使用数据库范围凭据上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
        [ FOR CRYPTOGRAPHIC PROVIDER cryptographic_provider_name ]  
```  
  
## <a name="arguments"></a>参数  
 *credential_name*  
 指定要创建的凭据的名称。 *credential_name*不能以数字 （#） 符号开头。 系统凭据以 ## 开头。  在使用共享的访问签名 (SAS) 时，此名称必须与容器路径匹配以 https 开头并且不能包含正斜杠。 请参阅示例 D 下面。  
  
 标识**=***identity_name*  
 指定从服务器外部进行连接时要使用的帐户名称。 当凭据用于访问 Azure 密钥保管库，**标识**是密钥保管库的名称。 请参阅以下示例 C。 使用共享的访问签名 (SAS) 凭据时**标识**是*共享访问签名*。 请参阅示例 D 下面。  
  
 机密**=***机密*  
 指定发送身份验证所需的机密内容。  
  
 当凭据用于访问 Azure 密钥保管库**机密**参数**CREATE CREDENTIAL**需要*\<客户端 ID >* （不带有连字符）和*\<机密 >*的**服务主体**一起无空格之间传递这些 Azure Active Directory 中。 请参阅以下示例 C。 凭据使用共享的访问签名时,**机密**是共享的访问签名令牌。 请参阅示例 D 下面。  有关在 Azure 的容器上创建存储的访问策略和共享的访问签名的信息，请参阅[第 1 课： 在 Azure 的容器上创建存储的访问策略和共享的访问签名](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)。  
  
 加密提供程序*cryptographic_provider_name*  
 指定的名称*企业密钥管理提供程序 (EKM)*。 有关密钥管理的详细信息，请参阅[可扩展密钥管理 &#40;Ekm&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>注释  

 当 IDENTITY 为 Windows 用户时，机密内容可以是密码。 机密内容使用服务主密钥进行加密。 如果重新生成服务主密钥，则使用新的服务主密钥重新加密机密内容。  
  
 在创建后一个凭据，你可以将其映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过使用登录[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)或[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)。 A[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名可以映射到一个凭据，但单个凭据可映射到多个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名。 有关详细信息，请参阅[凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)。 服务器级别凭据只能映射到登录名，不向数据库用户。 
  
 有关凭据的信息会显示在[sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)目录视图。  
  
 如果该提供程序没有任何登录名映射的凭据，则使用映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户的凭据。  
  
 一个登录名可以有多个映射的凭据，只要它们用于不同的提供程序即可。 每个登录名的每个提供程序只能有一个映射的凭据。 相同的凭据可以映射到其他登录名。  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER ANY CREDENTIAL**权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-basic-example"></a>A. 基本示例  
 以下示例创建名为 `AlterEgo` 的凭据。 凭据包含 Windows 用户 `Mary5` 和一个密码。  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>B. 创建用于 EKM 的凭据  
 下例使用一个名为 `User1OnEKM` 的帐户，它是以前通过 EKM 的管理工具在 EKM 模块中创建的，并带有一个基本帐户类型和密码。 **Sysadmin**服务器上的帐户创建凭据，可用于连接到 EKM 帐户中，并将它分配给`User1`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]帐户：  
  
```  
CREATE CREDENTIAL CredentialForEKM  
    WITH IDENTITY='User1OnEKM', SECRET='<EnterStrongPasswordHere>'  
    FOR CRYPTOGRAPHIC PROVIDER MyEKMProvider;  
GO  
  
/* Modify the login to assign the cryptographic provider credential */  
ALTER LOGIN Login1  
ADD CREDENTIAL CredentialForEKM;  
  
/* Modify the login to assign a non cryptographic provider credential */   
ALTER LOGIN Login1  
WITH CREDENTIAL = AlterEgo;  
GO  
```  
  
### <a name="c-creating-a-credential-for-ekm-using-the-azure-key-vault"></a>C. 使用 Azure 密钥保管库创建用于 EKM 的凭据  
 下面的示例创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]凭据[!INCLUDE[ssDE](../../includes/ssde-md.md)]访问 Azure 密钥保管库使用时要使用**Microsoft Azure 密钥保管库的 SQL Server 连接器**。 有关使用的完整示例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接器，请参阅[可扩展密钥管理使用 Azure Key Vault &#40;SQL server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  **CREATE CREDENTIAL** 的 **IDENTITY** 参数需要 key vault 名称。 **机密**参数**CREATE CREDENTIAL**需要*\<客户端 ID >* （不带有连字符） 和*\<密钥 >*一起无空格之间传递它们。  
  
 在下例中， **客户端 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) 去掉了连字符，并输入为字符串 `EF5C8E094D2A4A769998D93440D8115D` ，而 **Secret** 则表示为字符串 *SECRET_DBEngine*。  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 下面的示例使用变量创建相同的凭据**客户端 ID**和**机密**字符串，然后连接在一起形成**机密**自变量。 **替换**函数用于删除连字符，从客户端 id。  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>D. 创建使用 SAS 令牌的凭据  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)。  
  
 下面的示例创建使用 SAS 令牌的共享的访问签名凭据。  有关在 Azure 的容器上创建存储的访问策略和共享的访问签名，然后创建使用共享的访问签名的凭据的教程，请参阅[教程： 使用 SQL Server 2016 的 Microsoft Azure Blob 存储服务数据库](Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases.md)。  
  
> [!IMPORTANT]  
>  **凭据名称**参数需要的名称与容器路径匹配，以 https 开头并且不包含尾随正斜杠。 **标识**参数需要名称，*共享访问签名*。 **机密**参数需要共享的访问签名令牌。  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>另请参阅  
 [凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER 凭据 &#40;Transact SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [创建 DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [第 2 课： 创建使用共享的访问签名的 SQL Server 凭据](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [共享的访问签名](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  

