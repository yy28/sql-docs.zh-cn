---
title: "创建证书 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTIFICATE
- CREATE_CERTIFICATE_TSQL
- sql13.swb.createcertificate.f1
- CERTIFICATE_TSQL
- CREATE CERTIFICATE
- sql13.swb.certificateproperties.f1
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- certificates [SQL Server], adding
- certificates [SQL Server]
- adding certificates
- cryptography [SQL Server], certificates
- CREATE CERTIFICATE statement
ms.assetid: a4274b2b-4cb0-446a-a956-1c8e6587515d
caps.latest.revision: 74
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8753e820278eb04fff6f12e405d766fff5292e58
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-certificate-transact-sql"></a>CREATE CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的数据库添加证书。  
  
 此功能与使用数据层应用程序框架 (DACFx) 的数据库导出不兼容。 必须在导出之前删除所有证书。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE CERTIFICATE certificate_name [ AUTHORIZATION user_name ]   
    { FROM <existing_keys> | <generate_new_keys> }  
    [ ACTIVE FOR BEGIN_DIALOG =  { ON | OFF } ]  
  
<existing_keys> ::=   
    ASSEMBLY assembly_name  
    | {   
        [ EXECUTABLE ] FILE = 'path_to_file'  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]   
      }  
    | {   
        BINARY = asn_encoded_certificate  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]  
      }  
<generate_new_keys> ::=   
    [ ENCRYPTION BY PASSWORD = 'password' ]   
    WITH SUBJECT = 'certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<private_key_options> ::=  
      {   
        FILE = 'path_to_private_key'  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
    |  
      {   
        BINARY = private_key_bits  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
  
<date_options> ::=  
    START_DATE = 'datetime' | EXPIRY_DATE = 'datetime'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CERTIFICATE certificate_name   
    { <generate_new_keys> | FROM <existing_keys> }  
    [ ; ]  
  
<generate_new_keys> ::=   
    WITH SUBJECT ='certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<existing_keys> ::=   
    {   
      FILE ='path_to_file'  
      WITH PRIVATE KEY   
         (   
           FILE ='path_to_private_key'  
           , DECRYPTION BY PASSWORD ='password'   
         )  
    }  
  
<date_options> ::=  
    START_DATE ='datetime' | EXPIRY_DATE ='datetime'  
```  
  
## <a name="arguments"></a>参数  
 *certificate_name*  
 是在数据库中为证书的名称。  
  
 授权*user_name*  
 是拥有此证书的名称。  
  
 程序集*程序集 _ 名称*  
 指定已经加载到数据库中的已签名的程序集。  
  
 [可执行文件]文件 =*path_to_file*  
 指定包含证书的 DER 编码文件的完整路径（包括文件名）。 如果使用 EXECUTABLE 选项，则文件为已使用证书签名的 DLL。 *path_to_file*可以是本地路径或网络位置的 UNC 路径。 安全上下文中访问该文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务帐户。 该帐户必须具有所需的文件系统权限。  
  
 WITH PRIVATE KEY  
 指定将证书的私钥加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。 该子句只有在通过文件创建证书时才有效。 若要加载程序集的私钥，使用[ALTER 证书](../../t-sql/statements/alter-certificate-transact-sql.md)。  
  
 文件 =*path_to_private_key*  
 指定私钥的完整路径（包括文件名）。 *path_to_private_key*可以是本地路径或网络位置的 UNC 路径。 安全上下文中访问该文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务帐户。 该帐户必须具有所需的文件系统权限。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 asn_encoded_certificate  
 指定为二进制常量的 ASN 编码证书位。  
  
 二进制 =*private_key_bits*  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定为二进制常量的专有键位。 这些位可采用加密形式。 如果加密，则用户必须提供解密密码。 不会对此密码执行密码策略检查。 私钥位应该采用 PVK 文件格式。  
  
 DECRYPTION BY PASSWORD =*key_password*  
 指定对从文件中检索的私钥进行解密所需的密码。 如果私钥受空密码的保护，则该子句为可选项。 建议不要将私钥保存到无密码保护的文件中。 如果密码是必需的但没有指定密码，该语句将失败。  
  
 ENCRYPTION BY PASSWORD =*密码*  
 指定用于加密私钥的密码。 只有在需要使用密码对证书进行加密时，才使用该选项。 如果省略此子句，使用数据库主密钥进行加密的私钥。 *密码*必须符合 Windows 密码策略要求的计算机的运行的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅 [Password Policy](../../relational-databases/security/password-policy.md)。  
  
 使用者 =*certificate_subject_name*  
 术语*主题*X.509 标准中定义引用证书的元数据中的字段。 使用者应该是不能超过 64 个字符，并强制实施此限制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 Linux 上。 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 Windows 上，该对象可以是长达 128 个字符。 当它们存储在目录中，但包含证书的二进制大型对象 (BLOB) 将保留完整的使用者的名称时，将被截断超过 128 个字符的主题。  
  
 START_DATE =*datetime*  
 证书生效的日期。 如果未指定，START_DATE 被设置为当前日期。 START_DATE 采用 UTC 时间，并且可以通过可转换为日期和时间的任何格式指定。  
  
 EXPIRY_DATE =*datetime*  
 证书过期的日期。 如果未指定，EXPIRY_DATE 设置为一年后 START_DATE 日期。 EXPIRY_DATE 采用 UTC 时间，并且可以通过可转换为日期和时间的任何格式指定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Service Broker 检查过期日期。 但是，过期不强制执行时将使用证书进行加密。  
  
 ACTIVE FOR BEGIN_DIALOG = { **ON** |关闭}  
 使证书可用于 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对话会话的发起方。 默认值为 ON。  
  
## <a name="remarks"></a>注释  
 证书是一个数据库级的安全对象，它遵循 X.509 标准并支持 X.509 V1 字段。 CREATE CERTIFICATE 可以通过文件或程序集加载证书。 该语句也可生成密钥对并创建自我签名的证书。  
  
 私钥必须是\<= 2500 个字节，以加密格式。 生成的私有密钥[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是 1024 位长时间通过[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，并且具有 2048 位长开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 从外部源导入的私钥的最小长度为 384 位，最大长度为 4,096 位。 导入的私钥的长度必须是 64 位的整数倍。 用于 TDE 的证书限于专用密钥大小 3456 比特。  
  
 存储证书的整个序列号，但仅第一个 16 字节出现在 sys.certificates 目录视图。  
  
 存储证书的整个颁发者字段，但仅 sys.certificates 中的第一个 884 字节目录视图。  
  
 私钥必须对应于由指定的公共密钥*certificate_name*。  
  
 当您通过容器创建证书时，可选择是否加载私钥。 但是当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成自我签名的证书时，始终会创建私钥。 默认情况下，私钥使用数据库主密钥进行加密。 如果数据库主密钥不存在，并且没有指定密码，该语句将失败。  
  
 使用数据库主密钥加密的私钥时不需要 ENCRYPTION BY PASSWORD 选项。 仅当使用密码加密的私钥时，请使用此选项。 如果未指定密码，则使用数据库主密钥对证书的私钥进行加密。 如果无法打开数据库主密钥，则省略此子句将导致错误。  
  
 如果使用数据库主密钥对私钥进行加密，则不一定必须指定解密密码。  
  
> [!NOTE]  
>  内置的加密和签名功能不会检查证书的过期日期。 使用这些功能的用户必须决定何时检查证书的过期日期。  
  
 可以通过使用创建证书的二进制说明[CERTENCODED &#40;Transact SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md)和[CERTPRIVATEKEY &#40;Transact SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)函数。 有关示例，使用**CERTPRIVATEKEY**和**CERTENCODED**若要将证书复制到另一个数据库，请参阅主题中的示例 B [CERTENCODED &#40;Transact SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 要求对数据库具有 CREATE CERTIFICATE 权限。 只有 Windows 登录名、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名和应用程序角色才能拥有证书。 其他组和角色不能拥有证书。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-self-signed-certificate"></a>A. 创建自我签名的证书  
 下面的示例创建名为 `Shipping04` 的证书。 该证书的私钥是使用一个密码来保护的。  
  
```  
CREATE CERTIFICATE Shipping04   
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
   WITH SUBJECT = 'Sammamish Shipping Records',   
   EXPIRY_DATE = '20201031';  
GO  
```  
  
### <a name="b-creating-a-certificate-from-a-file"></a>B. 通过文件创建证书  
 以下示例在数据库中创建证书，并从文件加载密钥对。  
  
```  
CREATE CERTIFICATE Shipping11   
    FROM FILE = 'c:\Shipping\Certs\Shipping11.cer'   
    WITH PRIVATE KEY (FILE = 'c:\Shipping\Certs\Shipping11.pvk',   
    DECRYPTION BY PASSWORD = 'sldkflk34et6gs%53#v00');  
GO   
```  
  
### <a name="c-creating-a-certificate-from-a-signed-executable-file"></a>C. 通过已签名的可执行文件创建证书  
  
```  
CREATE CERTIFICATE Shipping19   
    FROM EXECUTABLE FILE = 'c:\Shipping\Certs\Shipping19.dll';  
GO  
```  
  
 或者，您还可以先通过 `dll` 文件创建程序集，然后通过程序集创建证书。  
  
```  
CREATE ASSEMBLY Shipping19   
    FROM ' c:\Shipping\Certs\Shipping19.dll'   
    WITH PERMISSION_SET = SAFE;  
GO  
CREATE CERTIFICATE Shipping19 FROM ASSEMBLY Shipping19;  
GO  
```  
  
### <a name="d-creating-a-self-signed-certificate"></a>D. 创建自我签名的证书  
 下面的示例创建名为的证书`Shipping04`而无需指定加密密码。 此示例可用于与[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。
  
```  
CREATE CERTIFICATE Shipping04   
   WITH SUBJECT = 'Sammamish Shipping Records';  
GO  
```  
  
  
## <a name="see-also"></a>另请参阅  
 [ALTER CERTIFICATE &#40;Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [删除证书 &#40;Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE (Transact-SQL)](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [CERTENCODED &#40;Transact SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md)   
 [CERTPRIVATEKEY &#40;Transact SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
  
  



