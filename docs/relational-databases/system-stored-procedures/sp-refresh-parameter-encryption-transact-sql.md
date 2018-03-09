---
title: "sp_refresh_parameter_encryption (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sp_refresh_parameter_encryption
- sp_refresh_parameter_encryption_TSQL
- sys.sp_refresh_parameter_encryption
- sys.sp_refresh_parameter_encryption_TSQL
helpviewer_keywords:
- sp_refresh_parameter_encryption
- Always Encrypted, sp_refresh_parameter_encryption
ms.assetid: 00b44baf-fcf0-4095-aabe-49fa87e77316
caps.latest.revision: "3"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a9343880058cef4ef86ce16613bc43821e8e8a24
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="sprefreshparameterencryption-transact-sql"></a>sp_refresh_parameter_encryption (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

更新的参数指定的非架构绑定存储的过程、 用户定义函数、 视图、 DML 触发器、 数据库级 DDL 触发器或当前数据库中的服务器级 DDL 触发器的始终加密元数据。 

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sys.sp_refresh_parameter_encryption [ @name = ] 'module_name' 
    [ , [ @namespace = ] '<class>' ]
[ ; ]

<class> ::=
{ DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER }
```

## <a name="arguments"></a>参数

[  **@name =** ] *模块名*   
是存储过程、用户定义函数、视图、DML 触发器、数据库级 DDL 触发器或服务器级 DDL 触发器的名称。 *模块名*不能为公共语言运行时 (CLR) 存储过程或 CLR 函数。 *模块名*不能绑定到架构的。 *模块名*是`nvarchar`，无默认值。 *模块名*可以是多个部分组成的标识符，但只能引用当前数据库中的对象。

[  **@namespace =** ]  < 类 >    
是指定模块的类。 当*模块名*是 DDL 触发器，`<class>`是必需的。 `<class>` 为 `nvarchar(20)`。 有效输入包括`DATABASE_DDL_TRIGGER`和`SERVER_DDL_TRIGGER`。    

## <a name="return-code-values"></a>返回代码值  

0（成功）或非零数字（失败）


## <a name="remarks"></a>Remarks

模块的参数加密元数据将变得过期，，如果：   
* 加密属性的模块引用，已更新的表中的列。 例如，某一列已被删除，已添加具有相同的名称，但不同的加密类型、 加密密钥或加密算法的新列。  
* 模块引用与过时的参数加密元数据的另一个模块。  

如果修改了表的加密属性，`sp_refresh_parameter_encryption`为直接或间接引用表的所有模块都应运行。 未将移动到其调用方之前需要用户第一次刷新的内部模块的情况下，可以在这些模块按任意顺序调用此存储的过程。

`sp_refresh_parameter_encryption`不会影响任何权限，扩展属性，或`SET`与对象相关联的选项。 

若要刷新服务器级 DDL 触发器，可以在任何数据库的上下文中执行此存储过程。

>  [!NOTE]   
>  在运行时，将删除与对象关联的任何签名`sp_refresh_parameter_encryption`。

## <a name="permissions"></a>权限

需要`ALTER`模块上的权限和`REFERENCES`任何 CLR 用户定义类型和 XML 架构集合引用的对象的权限。   

当指定的模块是数据库级 DDL 触发器时，要求`ALTER ANY DATABASE DDL TRIGGER`当前数据库中的权限。    

服务器级 DDL 触发器指定的模块时，需要`CONTROL SERVER`权限。

使用定义的模块`EXECUTE AS`子句，`IMPERSONATE`上指定的主体必须具有权限。 通常，刷新对象不会更改其`EXECUTE AS`主体，除非使用定义了该模块`EXECUTE AS USER`和主体现在解析为不同的用户不是确实执行此操作时模块已创建的用户名称。
 
## <a name="examples"></a>示例

下面的示例创建一个表和引用表的过程、 配置始终加密，然后演示更改表和运行`sp_refresh_parameter_encryption`过程。  

首先创建初始表和引用表的存储的过程。
```sql
CREATE TABLE [Patients]([PatientID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11), 
    [FirstName] [nvarchar](50) NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [MiddleName] [nvarchar](50) NULL,
    [StreetAddress] [nvarchar](50) NOT NULL,
    [City] [nvarchar](50) NOT NULL,
    [ZipCode] [char](5) NOT NULL,
    [State] [char](2) NOT NULL,
    [BirthDate] [date] NOT NULL,
 CONSTRAINT [PK_Patients] PRIMARY KEY CLUSTERED 
(
    [PatientID] ASC
) WITH 
    (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, 
     IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, 
     ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY];
GO

CREATE PROCEDURE [find_patient] @SSN [char](11)
AS
BEGIN
    SELECT * FROM [Patients] WHERE SSN=@SSN
END;
GO
```

然后设置始终加密密钥。
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
       0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085
);
GO
```


最后我们将替换为加密的列，然后运行 SSN 列`sp_refresh_parameter_encryption`过程更新的始终加密组件。
```sql
ALTER TABLE [Patients] DROP COLUMN [SSN];
GO

ALTER TABLE [Patients] 
    ADD [SSN] [char](11) COLLATE Latin1_General_BIN2 
    ENCRYPTED WITH 
        (COLUMN_ENCRYPTION_KEY = [CEK1], 
        ENCRYPTION_TYPE = Deterministic, 
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') 
    NOT NULL;
GO

EXEC sp_refresh_parameter_encryption [find_patient];
GO
```

## <a name="see-also"></a>另请参阅 

[始终加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[始终加密向导](../../relational-databases/security/encryption/always-encrypted-wizard.md)   

