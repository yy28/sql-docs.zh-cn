---
title: "ALTER DATABASE SCOPED CREDENTIAL (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 91224c6e96fb3ee3962331ec6f378ea9aad1a5b5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  更改数据库属性范围的凭据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>参数  
 *credential_name*  
 指定正在更改的数据库范围凭据的名称。  
  
 标识**=***identity_name*  
 指定从服务器外部进行连接时要使用的帐户名称。 若要从 Azure Blob 存储导入文件，标识名称必须是`SHARED ACCESS SIGNATURE`。  有关共享的访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。  
    
  
 机密**=***机密*  
 指定发送身份验证所需的机密内容。 *机密*需从 Azure Blob 存储导入文件。 *机密*可能是可选的用于其他目的。   
>  [!WARNING]
>  SAS 密钥值可能会开始使用？（问号）。 如果你使用 SAS 密钥，你必须删除前导？。 否则可能会阻止你的工作。    
  
## <a name="remarks"></a>注释  
 当数据库范围凭据发生更改，这两者的值*identity_name*和*机密*将重置。 如果未指定可选参数 SECRET 的值，则存储的密码值将设置为 NULL。  
  
 使用服务主密钥对密码进行加密。 如果重新生成服务主密钥，则需要使用新服务主密钥对该密码重新加密。  
  
 有关数据库范围凭据的信息会显示在[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)目录视图。  
  
## <a name="permissions"></a>Permissions  
 需要`ALTER`凭据的权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. 密码的数据库更改范围的凭据  
 下面的示例更改名为数据库范围凭据中存储的机密`Saddles`。 数据库范围凭据包含 Windows 登录`RettigB`及其密码。 新密码添加到使用机密的子句的数据库范围凭据。  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 删除凭据的密码  
 下面的示例从名为数据库范围的凭据中移除密码`Frames`。 数据库范围凭据包含 Windows 登录名`Aboulrus8`和密码。 执行该语句后，数据库范围凭据将具有空密码，因为未指定密钥的选项。  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [创建 DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

