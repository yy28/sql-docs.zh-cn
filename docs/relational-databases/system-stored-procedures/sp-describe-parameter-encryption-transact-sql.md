---
title: sp_describe_parameter_encryption （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_parameter_encryption
- sp_describe_parameter_encryption_TSQL
- sys.sp_describe_parameter_encryption
- sys.sp_describe_parameter_encryption_TSQL
helpviewer_keywords:
- sp_describe_parameter_encryption
ms.assetid: 706ed441-2881-4934-8d5e-fb357ee067ce
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c4a4cfe5c86d39766bcd322b879172b00b33eb68
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73593705"
---
# <a name="sp_describe_parameter_encryption-transact-sql"></a>sp_describe_parameter_encryption （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  分析指定[!INCLUDE[tsql](../../includes/tsql-md.md)]的语句及其参数，以确定哪些参数与使用 Always Encrypted 功能保护的数据库列相对应。 返回与加密列对应的参数的加密元数据。  
  
## <a name="syntax"></a>语法  
  
```  
sp_describe_parameter_encryption   
    [ @tsql = ] N'Transact-SQL_batch' ,   
    [ @params = ] N'parameters'   
[ ;]  
```  
  
## <a name="arguments"></a>参数  
 [ \@tsql =]"Transact-sql SQL_batch"  
 一个或多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 Transact-sql SQL_batch 可以是 nvarchar （n）或 nvarchar （max）。  
  
 [ \@params =]N'parameters'  
 params 为 transact-sql 批处理的参数提供声明字符串，这与 sp_executesql 类似。 * \@* 参数可以为 nvarchar （n）或 nvarchar （max）。  
  
 一个字符串，其中包含已嵌入到[!INCLUDE[tsql](../../includes/tsql-md.md)]_batch 中的所有参数的定义。 字符串必须是 Unicode 常量或 Unicode 变量。 每个参数定义由参数名称和数据类型组成。 *n*是表示附加参数定义的占位符。 语句中指定的每个参数都必须在* \@params*中定义。 如果语句[!INCLUDE[tsql](../../includes/tsql-md.md)]中的语句或批处理不包含* \@参数，则无需参数。* 该参数的默认值为 NULL。  
  
## <a name="return-value"></a>返回值  
 0表示成功。 任何其他表示失败。  
  
## <a name="result-sets"></a>结果集  
 **sp_describe_parameter_encryption**返回两个结果集：  
  
-   描述为数据库列配置的加密密钥的结果集，指定[!INCLUDE[tsql](../../includes/tsql-md.md)]的语句的参数对应于。  
  
-   描述应如何加密特定参数的结果集。 此结果集引用第一个结果集中所述的键。  
  
 第一个结果集的每一行描述一对键;加密的列加密密钥及其对应的列主密钥。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_ordinal**|**int**|结果集中的行的 Id。|  
|database_id |**int**|数据库 id。|  
|**column_encryption_key_id**|**int**|列加密密钥 id。注意：此 id 在[sys. column_encryption_keys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)目录视图中表示一行。|  
|**column_encryption_key_version**|**int**|保留供将来使用。 当前，始终包含1。|  
|**column_encryption_key_metadata_version**|**binary （8）**|表示列加密密钥的创建时间的时间戳。|  
|**column_encryption_key_encrypted_value**|**varbinary （4000）**|列加密密钥的加密值。|  
|**column_master_key_store_provider_name**|**sysname**|包含列主密钥的密钥存储的提供程序的名称，该列用于生成列加密密钥的加密值。|  
|**column_master_key_path**|**nvarchar(4000)**|列主密钥的密钥路径，该密钥用于生成列加密密钥的加密值。|  
|**column_encryption_key_encryption_algorithm_name**|**sysname**|用于生成列加密密钥的加密值的加密算法的名称。|  
  
 第二个结果集的每一行都包含一个参数的加密元数据。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int**|结果集中行的 Id。|  
|**parameter_name**|**sysname**|Params 参数中指定的其中一个参数的名称。 * \@*|  
|**column_encryption_algorithm**|**tinyint**|指示为列配置的加密算法的代码，参数对应于。 当前支持的值为：2表示**AEAD_AES_256_CBC_HMAC_SHA_256**。|  
|**column_encryption_type**|**tinyint**|指示为列配置的加密类型的代码，参数对应于。 支持的值包括：<br /><br /> 0-纯文本（列未加密）<br /><br /> 1-随机加密<br /><br /> 2-确定性加密。|  
|**column_encryption_key_ordinal**|**int**|第一个结果集中的行的代码。 引用的行描述为列配置的列加密密钥，参数对应于。|  
|**column_encryption_normalization_rule_version**|**tinyint**|类型规范化算法的版本号。|  
  
## <a name="remarks"></a>备注  
 支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Always Encrypted 的客户端驱动程序将自动调用**sp_describe_parameter_encryption**来检索由应用程序发出的参数化查询的加密元数据。 随后，驱动程序使用加密元数据对与 Always Encrypted 保护的数据库列对应的参数值进行加密，并使用加密的参数值，然后将查询发送到数据库引擎。  
  
## <a name="permissions"></a>权限  
 需要**查看任意列加密密钥定义**，并查看数据库中的**任何列主密钥定义**权限。  
  
## <a name="examples"></a>示例  
  
```sql  
CREATE COLUMN MASTER KEY [CMK1]  
WITH  
(  
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',  
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'  
);  
GO  
  
CREATE COLUMN ENCRYPTION KEY [CEK1]  
WITH VALUES  
(  
       COLUMN_MASTER_KEY = [CMK1],  
    ALGORITHM = 'RSA_OAEP',  
    ENCRYPTED_VALUE =   
0x016E000001630075007200720065006E00740075007300650072002F006D007  
9002F00610036003600620062003000660036006400640037003000620064006  
6006600300032006200360032006400300066003800370065003300340030003  
200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF991  
37B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA51  
7A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6  
686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015B  
DB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8  
C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE3  
74DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A3472  
3276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550E  
C5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E0  
35175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D8  
01ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B  
4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF8  
1A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202F  
C24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B0195883360  
4707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E  
9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C  
3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085  
);  
GO  
  
CREATE TABLE t1 (  
c1 INT ENCRYPTED WITH (  
    COLUMN_ENCRYPTION_KEY = [CEK_Auto1],   
    ENCRYPTION_TYPE = Randomized,   
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL,  
);  
  
EXEC sp_describe_parameter_encryption N'INSERT INTO t1 VALUES(@c1)',  N'@c1 INT';  
```  
  
 下面是第一个结果集：  
  
|column_encryption_key_ordinal|database_id|column_encryption_key_id|column_encryption_key_version|column_encryption_key_metadata_version|column_encryption_key_encrypted_value|  
|--------------------------------------|------------------|---------------------------------|--------------------------------------|------------------------------------------------|-----------------------------------------------|  
|1|5|1|1|0x99EDA60083A50000|0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085|  
  
 （结果继续。）  
  
|column_master_key_store_provider_name|column_master_key_path|column_encryption_key_encryption_algorithm_name|  
|------------------------------------------------|-------------------------------|----------------------------------------------------------|  
|MSSQL_CERTIFICATE_STORE|CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305|RSA_OAEP|  
  
 下面是第二个结果集：  
  
|parameter_ordinal|parameter_name|column_encryption_algorithm|column_encryption_type|  
|------------------------|---------------------|-----------------------------------|------------------------------|  
|1|\@低耗|1|1|  
  
 （结果继续。）  
  
|column_encryption_key_ordinal|column_encryption_normalization_rule_version|  
|--------------------------------------|------------------------------------------------------|  
|1|1|  
  
## <a name="see-also"></a>另请参阅  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [使用 Always Encrypted 开发应用程序](../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
