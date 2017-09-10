---
title: "更改列加密密钥 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER COLUMN ENCRYPTION
- ALTER_COLUMN_ENCRYPTION_TSQL
- ALTER COLUMN ENCRYPTION KEY
- ALTER_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column encryption key, alter
- ALTER COLUMN ENCRYPTION KEY statement
ms.assetid: c79a220d-e178-4091-a330-c924cc0f0ae0
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6aaa1f85f860272cdb672d29bccdda39380f728a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-column-encryption-key-transact-sql"></a>ALTER COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  更改列加密密钥在数据库中，添加或删除加密的值。 CEK 可以具有最多两个值用于进行相应的列主密钥的轮换。 加密使用的列时使用 CEK[始终加密 &#40; 数据库引擎 &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)功能。 在添加之前 CEK 值，必须定义列主密钥用于加密值，通过使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)语句。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ALTER COLUMN ENCRYPTION KEY key_name   
    [ ADD | DROP ] VALUE   
    (  
        COLUMN_MASTER_KEY = column_master_key_name   
        [, ALGORITHM = 'algorithm_name' , ENCRYPTED_VALUE =  varbinary_literal ]   
    ) [;]  
```  
  
## <a name="arguments"></a>参数  
 *key_name*  
 要更改列加密密钥。  
  
 *column_master_key_name*  
 指定用于加密列加密密钥 (CEK) 的列主密钥 (CMK) 的名称。  
  
 *algorithm_name*  
 用于加密值的加密算法的名称。 系统提供的算法必须**RSA_OAEP**。 删除列加密密钥值时，此自变量无效。  
  
 *varbinary_literal*  
 加密 CEK BLOB 与指定的主加密密钥。 实例时都提供 SQL Server 登录名。 删除列加密密钥值时，此自变量无效。  
  
> [!WARNING]  
>  决不要将传递纯文本 CEK 值在此语句中。 这样将构成此功能的好处。  
  
## <a name="remarks"></a>注释  
 通常情况下，使用一个加密值创建列加密密钥。 当列主密匙需要要旋转 （当前列主密钥需要将替换为新的列主密钥），你可以添加新值的列加密密钥，使用新的列主密钥加密。 这将允许你以确保客户端应用程序可以访问新的列主密钥在进行对客户端应用程序可用时使用的列加密密钥加密的数据。 驱动程序的客户端应用程序不具有对新的主密钥的访问，将能够使用旧列主密钥加密列加密密钥值访问敏感数据中启用了始终加密。 加密算法，始终加密支持的功能，需要具有 256 位的纯文本值。 应使用密钥存储提供程序，用于封装包含列主密钥的密钥存储生成的加密的值。  
  
 使用[sys.columns &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)， [sys.column_encryption_keys &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)和[sys.column_encryption_key_values &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)若要查看有关列加密密钥的信息。  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER ANY COLUMN ENCRYPTION KEY**对数据库拥有权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-adding-a-column-encryption-key-value"></a>A. 添加的列加密密钥值  
 以下示例更改列加密密钥调用`MyCEK`。  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
ADD VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK2,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0064006500650063006200660034006100340031003000380034006200350033003200360066003200630062006200350030003600380065003900620061003000320030003600610037003800310066001DDA6134C3B73A90D349C8905782DD819B428162CF5B051639BA46EC69A7C8C8F81591A92C395711493B25DCBCCC57836E5B9F17A0713E840721D098F3F8E023ABCDFE2F6D8CC4339FC8F88630ED9EBADA5CA8EEAFA84164C1095B12AE161EABC1DF778C07F07D413AF1ED900F578FC00894BEE705EAC60F4A5090BBE09885D2EFE1C915F7B4C581D9CE3FDAB78ACF4829F85752E9FC985DEB8773889EE4A1945BD554724803A6F5DC0A2CD5EFE001ABED8D61E8449E4FAA9E4DD392DA8D292ECC6EB149E843E395CDE0F98D04940A28C4B05F747149B34A0BAEC04FFF3E304C84AF1FF81225E615B5F94E334378A0A888EF88F4E79F66CB377E3C21964AACB5049C08435FE84EEEF39D20A665C17E04898914A85B3DE23D56575EBC682D154F4F15C37723E04974DB370180A9A579BC84F6BC9B5E7C223E5CBEE721E57EE07EFDCC0A3257BBEBF9ADFFB00DBF7EF682EC1C4C47451438F90B4CF8DA709940F72CFDC91C6EB4E37B4ED7E2385B1FF71B28A1D2669FBEB18EA89F9D391D2FDDEA0ED362E6A591AC64EF4AE31CA8766C259ECB77D01A7F5C36B8418F91C1BEADDD4491C80F0016B66421B4B788C55127135DA2FA625FB7FD195FB40D90A6C67328602ECAF3EC4F5894BFD84A99EB4753BE0D22E0D4DE6A0ADFEDC80EB1B556749B4A8AD00E73B329C95827AB91C0256347E85E3C5FD6726D0E1FE82C925D3DF4A9  
);  
GO  
  
```  
  
### <a name="b-dropping-a-column-encryption-key-value"></a>B. 删除列加密密钥值  
 以下示例更改列加密密钥调用`MyCEK`通过将一个值。  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
DROP VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK  
);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact SQL &#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_encryption_key_values (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  

