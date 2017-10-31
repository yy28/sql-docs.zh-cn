---
title: "创建非对称密钥 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE SYMMETRIC KEY
- SYMMETRIC KEP
- CREATE_SYMMETRIC_KEY_TSQL
- SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SYMMETRIC KEY statement
- temporary symmetric keys [SQL Server]
- symmetric keys [SQL Server], creating
- symmetric keys [SQL Server]
ms.assetid: b5d23572-b79d-4cf1-9eef-d648fa3b1358
caps.latest.revision: 72
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: d3b1490b1ac07d0e6a3f0fc3ed1515dd0872d545
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="create-symmetric-key-transact-sql"></a>CREATE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中生成对称密钥并指定其属性。  
  
 此功能与使用数据层应用程序框架 (DACFx) 的数据库导出不兼容。 必须在导出之前删除所有对称密钥。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE SYMMETRIC KEY key_name   
    [ AUTHORIZATION owner_name ]  
    [ FROM PROVIDER provider_name ]  
    WITH 
      [
          <key_options> [ , ... n ]  
        | ENCRYPTION BY <encrypting_mechanism> [ , ... n ] 
      ]
  
<key_options> ::=  
      KEY_SOURCE = 'pass_phrase'  
    | ALGORITHM = <algorithm>  
    | IDENTITY_VALUE = 'identity_phrase'  
    | PROVIDER_KEY_NAME = 'key_name_in_provider'   
    | CREATION_DISPOSITION = {CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
    DES | TRIPLE_DES | TRIPLE_DES_3KEY | RC2 | RC4 | RC4_128  
    | DESX | AES_128 | AES_192 | AES_256   
  
<encrypting_mechanism> ::=  
      CERTIFICATE certificate_name   
    | PASSWORD = 'password'   
    | SYMMETRIC KEY symmetric_key_name   
    | ASYMMETRIC KEY asym_key_name  
```  
  
## <a name="arguments"></a>参数  
 *Key_name*  
 指定在数据库中识别该对称密钥的唯一名称。 临时密钥的名称应当以数字符号 (#) 开头。 例如， **#temporaryKey900007**。 您不能创建名称以多个 # 开头的对称密钥。 您不能使用 EKM 提供程序创建临时对称密钥。  
  
 授权*owner_name*  
 指定将拥有此密钥的数据库用户或应用程序角色的名称。  
  
 从提供程序*provider_name*  
 指定可扩展密钥管理 (EKM) 提供程序和名称。 该密钥不是从 EKM 设备中导出的。 必须先使用 CREATE PROVIDER 语句定义此提供程序。 有关创建外部密钥的提供程序的详细信息，请参阅[可扩展密钥管理 &#40;Ekm&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 KEY_SOURCE **=***pass_phrase*  
 指定从中派生密钥的通行短语。  
  
 IDENTITY_VALUE **=***identity_phrase*  
 指定一个标识短语，将根据该短语生成 GUID 以标记使用临时密钥加密的数据。  
  
 PROVIDER_KEY_NAME**=***key_name_in_provider*  
 指定在可扩展密钥管理提供程序中引用的名称。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 CREATION_DISPOSITION ** = ** CREATE_NEW  
 在可扩展的密钥管理设备上创建新密钥。  如果密钥已存在于设备上，该语句将失败，并显示错误。  
  
 CREATION_DISPOSITION ** = ** OPEN_EXISTING  
 将一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对称密钥映射到现有的可扩展密钥管理密钥。 如果未提供 CREATION_DISPOSITION = OPEN_EXISTING，则此参数默认为 CREATE_NEW。  
  
 *certificate_name*  
 指定将用于对对称密钥进行加密的证书的名称。 该证书必须已存在于数据库中。  
  
  *密码*   
 指定一个密码，从该密码派生出用来保护对称密钥的 TRIPLE_DES 密钥。 *密码*必须符合 Windows 密码策略要求的计算机的运行的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 始终使用强密码。  
  
 *symmetric_key_name*  
 指定对称密钥，使用正在创建的密钥进行加密。 指定的密钥必须已存在于数据库中，并且必须打开。  
  
 *asym_key_name*  
 指定一个非对称密钥用于加密正在创建的密钥。 此非对称密钥必须已经存在于数据库中。  
  
 \<算法 >  
指定的加密算法。   
> [!WARNING]  
> 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]开始，除 AES_128、AES_192 和 AES_256 以外的所有算法都已过时。 若要使用较旧算法 （不推荐），必须设置数据库到数据库兼容性级别 120 或更低。  
  
## <a name="remarks"></a>注释  
 创建对称密钥时，必须至少使用以下项之一来对该对称密钥进行加密：证书、密码、对称密钥、非对称密钥或 PROVIDER。 可使用上述每种类型中的多项对密钥进行加密。 换言之，可以同时使用多个证书、密码、对称密钥以及非对称密钥对单个对称密钥进行加密。  
  
> [!CAUTION]  
>  当使用密码（而不是数据库主密钥的公钥）对对称密钥进行加密时，便会使用 TRIPLE DES 加密算法。 因此，用强加密算法（如 AES）创建的密钥本身受较弱算法的保护。  
  
 在将对称密钥分发给多个用户之前，可以使用可选的密码对该密钥进行加密。  
  
 临时密钥由创建它们的用户所拥有。 临时密钥只对当前会话有效。  
  
 IDENTITY_VALUE 生成一个 GUID，使用该 GUID 来标记使用新对称密钥加密的数据。 该标记可用于将密钥与加密数据进行匹配。 由特定短语生成的 GUID 始终是相同的。 在使用短语生成了 GUID 之后，只要存在至少一个正在使用该短语的会话，就不能再次使用该短语。 IDENTITY_VALUE 是一个可选的子句；但是，我们建议在存储使用临时密钥加密的数据时使用该子句。  
  
 没有默认的加密算法。  
  
> [!IMPORTANT]  
>  建议不要使用 RC4 和 RC4_128 序列密码保护敏感数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对利用此类密钥执行的加密不会进行进一步的编码。  
  
 有关对称密钥的信息会显示在[sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)目录视图。  
  
 使用通过加密提供程序创建的对称密钥无法加密对称密钥。  
  
 **关于 DES 算法的说明：**  
  
-   DESX 的命名不正确。 使用 ALGORITHM = DESX 创建的对称密钥实际上使用的是具有 192 位密钥的 TRIPLE DES 密码。 不提供 DESX 算法。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
-   使用 ALGORITHM = TRIPLE_DES_3KEY 创建的对称密钥使用的是具有 192 位密钥的 TRIPLE DES。  
-   使用 ALGORITHM = TRIPLE_DES 创建的对称密钥使用的是具有 128 位密钥的 TRIPLE DES。  
  
 **不是推荐使用 RC4 算法：**  
  
 重复的使用相同的 RC4 或 RC4_128 KEY_GUID 上不同的数据，块导致在相同的 RC4 密钥，因为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不自动提供 salt。 重复使用相同的 RC4 密钥是已知错误，将导致加密非常不可靠。 因此，不推荐使用 RC4 和 RC4_128 关键字。 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!WARNING]  
>  RC4 算法仅用于支持向后兼容性。 仅当数据库兼容级别为 90 或 100 时，才能使用 RC4 或 RC4_128 对新材料进行加密。 （建议不要使用。）而是使用一种较新的算法，如 AES 算法之一。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，可以通过任何兼容级别对使用 RC4 或 RC4_128 加密的材料进行解密。  
  
## <a name="permissions"></a>Permissions  
 要求对数据库具有 ALTER ANY SYMMETRIC KEY 权限。 如果指定了 AUTHORIZATION，则要求对数据库用户具有 IMPERSONATE 权限，或者对应用程序角色具有 ALTER 权限。 如果使用证书或非对称密钥进行加密，则要求对证书或非对称密钥具有 VIEW DEFINITION 权限。 只有 Windows 登录名、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和应用程序角色才能拥有对称密钥。 其他组和角色不能拥有对称密钥。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-symmetric-key"></a>A. 创建对称密钥  
 下面的示例使用 `JanainaKey09` 算法创建名为 `AES 256` 的对称密钥，然后使用证书 `Shipping04` 对新密钥进行加密。  
  
```  
CREATE SYMMETRIC KEY JanainaKey09   
WITH ALGORITHM = AES_256  
ENCRYPTION BY CERTIFICATE Shipping04;  
GO  
```  
  
### <a name="b-creating-a-temporary-symmetric-key"></a>B. 创建临时对称密钥  
 下面的示例用通行短语 `#MarketingXXV` 创建了一个名为 `The square of the hypotenuse is equal to the sum of the squares of the sides` 的临时对称密钥。 为该密钥提供了通过字符串 `Pythagoras` 生成的 GUID，并使用证书 `Marketing25` 对该密钥进行加密。  
  
```  
  
CREATE SYMMETRIC KEY #MarketingXXV   
WITH ALGORITHM = AES_128,  
KEY_SOURCE   
     = 'The square of the hypotenuse is equal to the sum of the squares of the sides',  
IDENTITY_VALUE = 'Pythagoras'  
ENCRYPTION BY CERTIFICATE Marketing25;  
GO  
```  
  
### <a name="c-creating-a-symmetric-key-using-an-extensible-key-management-ekm-device"></a>C. 使用可扩展密钥管理 (EKM) 设备创建对称密钥  
 下面的示例使用一个名为 `MySymKey` 的提供程序和一个密钥名称 `MyEKMProvider` 创建一个名为 `KeyForSensitiveData` 的对称密钥。 该示例向 `User1` 授权，并假定系统管理员已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册了名为 `MyEKMProvider` 的提供程序。  
  
```  
CREATE SYMMETRIC KEY MySymKey  
AUTHORIZATION User1  
FROM PROVIDER EKMProvider  
WITH  
PROVIDER_KEY_NAME='KeyForSensitiveData',  
CREATION_DISPOSITION=OPEN_EXISTING;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.symmetric_keys &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [可扩展密钥管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [使用 Azure 密钥保管库的可扩展密钥管理 (SQL Server)](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  

