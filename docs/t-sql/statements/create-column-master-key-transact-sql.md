---
title: CREATE COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a4f7c950785268f1b462c8363e4fb9e5f426055b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993129"
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  在数据库中创建列主密钥元数据对象。 列主密钥元数据条目代表一个密钥，该密钥存储在外部密钥存储中，在使用 [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)功能时用于保护（加密）列加密密钥。 多列主密钥允许密钥轮换；定期更改密钥以增强安全性。 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的对象资源管理器或 PowerShell 在密钥存储中创建列主密钥，并在数据库中创建对应的元数据对象。 有关详细信息，请参阅 [Always Encrypted 密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。  
  
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
 key_name  
 列主密钥在数据库中所使用的名称。  
  
 key_store_provider_name  
 指定密钥存储提供程序的名称，该提供程序是一个客户端软件组件，用于封装包含列主密钥的密钥存储。 启用了 Always Encrypted 的客户端驱动程序使用密钥存储提供程序名称在密钥存储提供程序的驱动程序注册表中查找密钥存储提供程序。 驱动程序使用提供程序解密存储在基础密钥存储中并由列主密钥保护的列加密密钥。 然后使用列加密密钥的明文值来加密与加密数据库列相对应的查询参数，或者解密来自加密列的查询结果。  
  
 启用了 Always Encrypted 的客户端驱动程序库包括热门密钥存储的密钥存储提供程序。   
  
可用的提供程序集取决于客户端驱动程序的类型和版本。 有关特定驱动程序的信息，请参阅 Always Encrypted 文档：

[将 Always Encrypted 与用于 SQL Server 的 .NET Framework 提供程序配合使用来开发应用程序](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


下表收集了系统提供程序的名称：  
  
|密钥存储提供程序名称|基础密钥存储|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Windows 证书存储| 
    |'MSSQL_CSP_PROVIDER'|支持 Microsoft CryptoAPI 的存储，如硬件安全模块 (HSM)。|
    |'MSSQL_CNG_STORE'|支持下一代加密技术 API 的存储，如硬件安全模块 (HSM)。|  
    |'Azure_Key_Vault'|请参阅 [Azure Key Vault 入门](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 可以实现自定义密钥存储提供程序，以存储启用了 Always Encrypted 的客户端驱动程序中没有任何内置密钥存储提供程序的存储中的列主密钥。  请注意，自定义密钥存储提供程序的名称不能以 MSSQL_ 开头，因为它是为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 密钥存储提供程序保留的前缀。 

  
 key_path  
 列主密钥存储中的密钥路径。 密钥路径必须在每个客户端应用程序的上下文中有效（这些客户端应用程序预期用于加密或解密存储在列中、由被引用列主密钥（间接）保护的数据），并且客户端应用程序需要具有密钥访问权限。 密钥路径的格式特定于密钥存储提供程序。 以下列表描述了特定的 Microsoft 系统密钥存储提供程序的密钥路径的格式。  
  
-   提供程序名称：MSSQL_CERTIFICATE_STORE  
  
     密钥路径格式：CertificateStoreName/CertificateStoreLocation/CertificateThumbprint  
  
     其中：  
  
     CertificateStoreLocation  
     证书存储位置，必须为当前用户或本地计算机。 有关详细信息，请参阅 [Local Machine and Current User Certificate Stores](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx)（本地计算机和当前用户证书存储）。  
  
     CertificateStore  
     证书存储名称，例如 My。  
  
     CertificateThumbprint  
     证书指纹。  
  
     **示例：**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   提供程序名称：MSSQL_CSP_PROVIDER  
  
     密钥路径格式：ProviderName/KeyIdentifier  
  
     其中：  
  
     *ProviderName*  
     列主密钥存储的加密服务提供程序（CSP，用于实现 CAPI）的名称。 如果使用 HSM 作为密钥存储，则此名称必须是你的 HSM 供应商提供的 CSP 的名称。 提供程序必须安装在客户端计算机上。  
  
     KeyIdentifier  
     密钥存储中的密钥标识符，用作列主密钥。  
  
     **示例：**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   提供程序名称：MSSQL_CNG_STORE  
  
     密钥路径格式：ProviderName/KeyIdentifier  
  
     其中：  
  
     *ProviderName*  
     列主密钥存储的密钥存储提供程序（KSP，用于实现下一代加密技术 (CNG) API）的名称。 如果使用 HSM 作为密钥存储，则此名称必须是你的 HSM 供应商提供的 KSP 的名称。 提供程序需要安装在客户端计算机上。  
  
     KeyIdentifier  
     密钥存储中的密钥标识符，用作列主密钥。  
  
     **示例：**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   提供程序名称：AZURE_KEY_STORE  
  
     密钥路径格式：KeyUrl  
  
     其中：  
  
     KeyUrl  
     Azure Key Vault 中密钥的 URL


例如：
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>Remarks  

必须在列加密密钥元数据条目可以在数据库中创建之前，以及数据库中的任何列可以使用 Always Encrypted 加密之前，创建列主密钥元数据条目。 请注意，元数据中的列主密钥条目不包含实际的列主密钥，实际的列主密钥必须存储在外部列密钥存储（SQL Server 外部）中。 元数据中的密钥存储提供程序名称和列主密钥路径必须对客户端应用程序有效，以便能够使用列主密钥解密由列主密钥加密的列加密密钥，以及查询加密的列。


  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY COLUMN MASTER KEY 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-column-master-key"></a>A. 创建列主密钥  
 对于使用 MSSQL_CERTIFICATE_STORE 提供程序访问列主密钥的客户端应用程序，为存储在证书存储中的列主密钥创建列主密钥元数据条目：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 为由使用 MSSQL_CNG_STORE 提供程序的客户端应用程序访问的列主密钥创建列主密钥元数据条目：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 对于使用 AZURE_KEY_VAULT 提供程序的客户端应用程序，创建存储在 Azure Key Vault 中的列主密钥以访问列主密钥。  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 创建存储在自定义列主密钥存储中的 CMK：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>另请参阅
 
* [DROP COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [创建列加密密钥 (Transact-SQL)](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [Always Encrypted 密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  
