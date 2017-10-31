---
title: "创建列主密钥 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/18/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQL13.SWB.NEWCOLUMNMASTERKEYDEF.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEYDEF.GENERAL.F1
- CREATE COLUMN MASTER KEY
- COLUMN MASTER KEY
- CREATE_COLUMN_MASTER_KEY_TSQL
- COLUMN_MASTER_KEY_TSQL
- SQL13.SWB.NEWCOLUMNMASTERKEY.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEY.GENERAL.F1
dev_langs:
- TSQL
helpviewer_keywords:
- column master key definition
- column master key, create
- CREATE COLUMN MASTER KEY statement
- Always Encrypted, create column master key
ms.assetid: f8926b95-e146-4e3f-b56b-add0c0d0a30e
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 871acb46898a9a62b25062f69d4e51bf28658f06
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  在数据库中创建列主密钥元数据对象。 表示一个密钥，列主密钥元数据条目存储在外部存储，用于保护 （加密） 列加密密钥时使用[始终加密 &#40; 数据库引擎 &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)功能。 密钥轮换; 的允许多个列主密钥定期更改密钥以增强安全性。 你可以通过对象资源管理器中创建的密钥存储和数据库中其相应的元数据对象中列主密匙[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell。 有关详细信息，请参阅[密钥管理概述 Always encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
         )   
[;]  
```  
  
## <a name="arguments"></a>参数  
 *key_name*  
 是依据列主密钥将已知的数据库中的名称。  
  
 *key_store_provider_name*  
 指定的密钥存储提供程序，它是封装包含列主密钥的密钥存储的客户端软件组件的名称。 启用始终加密的客户端驱动程序使用密钥存储提供程序名称来查找的密钥存储提供程序的驱动程序的注册表中的密钥存储提供程序。 该驱动程序使用提供程序解密列加密密钥，受列主密匙，存储在基础的密钥存储。 列加密密钥的纯文本值然后用于加密查询参数，对应于加密的数据库列，或以解密从加密列的查询结果。  
  
 启用始终加密的客户端驱动程序库包含常用的密钥存储的密钥存储提供程序。   
  
可用的提供程序集依赖于类型和版本的客户端驱动程序。 请参阅特定驱动程序的始终加密文档：

[开发应用程序使用始终加密的.NET Framework 提供的 SQL Server](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


下表捕获系统提供程序的名称：  
  
|密钥存储提供程序名称|基础的密钥存储|  
    |-----------------------------|--------------------------|
    |MSSQL_CERTIFICATE_STORE|Windows 证书存储区| 
    |MSSQL_CSP_PROVIDER|存储区中，如支持 Microsoft CryptoAPI 硬件安全模块 (HSM)。|
    |MSSQL_CNG_STORE|存储区中的，例如硬件安全模块 (HSM)，支持加密 API： 下一代。|  
    |Azure_Key_Vault|请参阅[Getting Started with Azure 密钥保管库](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 你可以实现自定义密钥存储提供程序，以存储没有任何内置密钥存储中的列主密钥存储提供程序中启用始终加密的客户端驱动程序。  请注意，自定义密钥存储提供程序的名称不能以 MSSQL_，是一个前缀开头留待[!INCLUDE[msCoName](../../includes/msconame-md.md)]密钥存储提供程序。 

  
 key_path  
 路径中的列主密钥的密钥存储。 密钥路径必须是有效的预期要加密或解密数据 （间接） 引用的列主密钥保护列中存储每个客户端应用程序的上下文中，客户端应用程序需要有权访问该密钥。 密钥路径的格式是特定于密钥存储提供程序。 以下列表描述为特定的 Microsoft 系统密钥存储提供程序的密钥路径的格式。  
  
-   **提供程序名称：** MSSQL_CERTIFICATE_STORE  
  
     **密钥路径格式：** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     其中：  
  
     *CertificateStoreLocation*  
     证书存储位置，它必须是当前用户或本地计算机。 有关详细信息，请参阅[本地计算机和当前用户证书存储](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx)。  
  
     *CertificateStore*  
     证书存储名称，例如我。  
  
     *CertificateThumbprint*  
     证书指纹。  
  
     **示例：**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **提供程序名称：** MSSQL_CSP_PROVIDER  
  
     **密钥路径格式：** *ProviderName*/*KeyIdentifier*  
  
     其中：  
  
     *ProviderName*  
     名称的列主密钥存储实现 CAPI，加密服务提供程序 (CSP)。 如果 HSM 将用作密钥存储中时，这必须是 CSP HSM 供应商的名称提供。 必须在客户端计算机上安装提供程序。  
  
     *KeyIdentifier*  
     密钥标识符用作列主密钥的密钥存储中。  
  
     **示例：**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **提供程序名称：** MSSQL_CNG_STORE  
  
     **密钥路径格式：** *ProviderName*/*KeyIdentifier*  
  
     其中：  
  
     *ProviderName*  
     名称的密钥存储提供程序 (KSP)，这将实现加密： 下一代 (CNG) API，列主密钥存储。 如果 HSM 将用作密钥存储中时，这必须是 KSP HSM 供应商的名称提供。 需要客户端计算机上安装提供程序。  
  
     *KeyIdentifier*  
     密钥标识符用作列主密钥的密钥存储中。  
  
     **示例：**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **提供程序名称：** AZURE_KEY_STORE  
  
     **密钥路径格式：** *KeyUrl*  
  
     其中：  
  
     *KeyUrl*  
     Azure 密钥保管库中密钥的 URL


例如：
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>注释  

在数据库中，可以使用始终加密对数据库中的任何列进行加密之前，可以创建列加密密钥元数据条目之前，创建列主密钥元数据条目是必需的。 请注意，元数据中的列主密钥条目不包含实际的列主密钥必须存储在外部列的密钥存储区 （在外部 SQL Server)。 密钥存储提供程序名称和元数据中的列主密钥路径必须是有效的客户端应用程序要能够使用列主密钥，使用列主密钥加密列加密密钥进行解密并查询加密的列。


  
## <a name="permissions"></a>Permissions  
 需要**更改任意列主密钥**权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-column-master-key"></a>A. 创建列主密钥  
 创建列主密钥的客户端应用程序使用 MSSQL_CERTIFICATE_STORE 提供程序访问列主密钥存储在证书存储，列主密钥元数据条目：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 创建使用 MSSQL_CNG_STORE 提供程序的客户端应用程序访问列主密钥的列主密钥元数据条目：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 创建列主密钥存储在 Azure 密钥保管库，AZURE_KEY_VAULT 提供程序，用于访问列主密钥的客户端应用程序。  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 创建自定义列主密钥存储中存储 CMK:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>另请参阅
 
* [删除列主密钥 &#40;Transact SQL &#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [创建列加密密钥 (Transact-SQL)](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [Always Encrypted 密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  

