---
title: "创建非对称密钥 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f39a31a9b2de4cd8153fa617b9cab1c1235f2a7a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在数据库中创建非对称密钥。  
  
 此功能与使用数据层应用程序框架 (DACFx) 的数据库导出不兼容。 必须在导出之前删除所有非对称密钥。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE ASYMMETRIC KEY Asym_Key_Name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <Asym_Key_Source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<Asym_Key_Source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY Assembly_Name  
   | PROVIDER Provider_Name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>参数  
 从*Asym_Key_Source*  
 指定从中加载非对称密钥对的源。  
  
 授权*database_principal_name*  
 指定非对称密钥的所有者。 所有者不能是角色或组。 如果省略该选项，则所有者为当前用户。  
  
 文件 =*path_to_strong name_file*  
 指定从中加载密钥对的强名称文件所在的路径。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 可执行文件 =*path_to_executable_file*  
 指定从中加载公钥的程序集文件。 由 MAX_PATH 根据 Windows API 限制为 260 个字符。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 程序集*程序集 _ 名称*  
 指定从中加载公钥的程序集的名称。  
  
加密通过 *\<key_name_in_provider >*指定如何加密密钥。 可以为证书、密码或非对称密钥。  
  
 KEY_NAME =*key_name_in_provider*  
 指定来自外部提供程序的密钥名称。 有关外部密钥管理的详细信息，请参阅[可扩展密钥管理 &#40;Ekm&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 CREATION_DISPOSITION = CREATE_NEW  
 在可扩展的密钥管理设备上创建新密钥。 PROV_KEY_NAME 必须用于指定设备上的密钥名称。 如果密钥已存在于设备上，此语句将失败，并显示错误。  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 地图[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到现有的可扩展密钥管理密钥的非对称密钥。 PROV_KEY_NAME 必须用于指定设备上的密钥名称。 如果未提供 CREATION_DISPOSITION = OPEN_EXISTING，则默认值为 CREATE_NEW。  
  
 算法 =\<算法 >  
 可以提供五个算法;RSA_4096、 RSA_3072、 RSA_2048、 RSA_1024 和 RSA_512。  
  
 RSA_1024 和 RSA_512 已弃用。 若要使用 RSA_1024 或 RSA_512 （不推荐） 你必须设置数据库到数据库兼容性级别 120 或更低。  
  
 密码 =*密码*  
 指定用于对私钥进行加密的密码。 如果未提供该子句，则使用数据库主密钥对私钥进行加密。 *密码*最多 128 个字符。 *密码*必须符合 Windows 密码策略要求的计算机的运行的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="remarks"></a>注释  
 *非对称密钥*是在数据库级别的安全对象的实体。 该实体的默认格式包含公钥和私钥。 当未使用 FROM 子句执行时，CREATE ASYMMETRIC KEY 会生成新的密钥对。 当使用 FROM 子句执行时，CREATE ASYMMETRIC KEY 会从文件中导入密钥对，或从程序集中导入公钥。  
  
 默认情况下，私钥受数据库主密钥保护。 如果尚未创建任何数据库主密钥，则需要使用密码保护私钥。 如果不存在数据库主密钥，则可以选择性地使用密码。  
  
 私钥的长度可以为 512、1024 或 2048 位。  
  
## <a name="permissions"></a>Permissions  
 需要对数据库拥有 CREATE ASYMMETRIC KEY 权限。 如果指定了 AUTHORIZATION 子句，则需要对数据库主体具有 IMPERSONATE 权限，或者对应用程序角色具有 ALTER 权限。 只有 Windows 登录名、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名和应用程序角色才能拥有对称密钥。 其他组和角色不能拥有非对称密钥。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-an-asymmetric-key"></a>A. 创建非对称密钥  
 下面的示例使用 `PacificSales09` 算法创建名为 `RSA_2048` 的非对称密钥，并使用密码保护私钥。  
  
```  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>B. 通过文件创建非对称密钥，为用户提供授权  
 以下示例通过文件中存储的密钥对创建非对称密钥 `PacificSales19`，然后授权用户 `Christina` 使用该非对称密钥。  
  
```  
CREATE ASYMMETRIC KEY PacificSales19 AUTHORIZATION Christina   
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp'    
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>C. 通过 EKM 提供程序创建非对称密钥  
 下面的示例从存储在文件中的密钥对创建非对称密钥 `EKM_askey1`。 然后，使用名为 `EKMProvider1` 的可扩展的密钥管理提供程序和该提供程序中名为 `key10_user1` 的密钥对其进行加密。  
  
```  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [使用 Azure 密钥保管库的可扩展密钥管理 (SQL Server)](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  

