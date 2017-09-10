---
title: "创建 DATABASE SCOPED CREDENTIAL (Transact SQL) |Microsoft 文档"
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
- DATABASE SCOPED CREDENTIAL
- DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_TSQL
- CREATE_DATABASE_SCOPED_CREDENTIAL
- CREATE_DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL
helpviewer_keywords:
- DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], DATABASE SCOPED CREDENTIAL statement
ms.assetid: fe830577-11ca-44e5-953b-2d589d54d045
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7e1eeda5d365f5c625e68c498c741754bf59c9d7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-scoped-credential-transact-sql"></a>创建 DATABASE SCOPED CREDENTIAL (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  创建数据库的凭据。 数据库的凭据未映射到服务器登录名或数据库用户。 凭据是数据库用于访问到外部位置中，每当数据库执行需要访问的操作。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
 
CREATE DATABASE SCOPED CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
  
```  
  
## <a name="arguments"></a>参数  
 *credential_name*  
 指定要创建的数据库范围凭据的名称。 *credential_name*不能以数字 （#） 符号开头。 系统凭据以 ## 开头。  
  
 标识**=***identity_name*  
 指定从服务器外部进行连接时要使用的帐户名称。 若要从 Azure Blob 存储导入文件，标识名称必须是`SHARED ACCESS SIGNATURE`。  有关共享的访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。  
  
 机密**=***机密*  
 指定发送身份验证所需的机密内容。 `SECRET`需要从 Azure Blob 存储导入文件。   
>  [!WARNING]
>  SAS 密钥值可能会开始使用？（问号）。 如果你使用 SAS 密钥，你必须删除前导？。 否则可能会阻止你的工作。  
  
## <a name="remarks"></a>注释  
 数据库范围的凭据是包含连接到外部的资源所需的身份验证信息的记录[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 多数凭据包括一个 Windows 用户和一个密码。  
  
 创建数据库范围的凭据之前，数据库必须具有主密钥来保护凭据。 有关详细信息，请参阅 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)。  
  
 当 IDENTITY 为 Windows 用户时，机密内容可以是密码。 机密内容使用服务主密钥进行加密。 如果重新生成服务主密钥，则使用新的服务主密钥重新加密机密内容。  
   
 有关数据库范围凭据的信息会显示在[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)目录视图。  
  
 
 Hereare 数据库的一些应用程序范围的凭据：  
  
- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]使用数据库范围的凭据来访问非公共 Azure blob 存储或使用 PolyBase 的 Kerberos 保护的 Hadoop 群集。 若要了解详细信息，请参阅[CREATE EXTERNAL DATA SOURCE (TRANSACT-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)。  

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]使用 PolyBase 的数据库范围的凭据以访问非公共 Azure blob 存储。 若要了解详细信息，请参阅[CREATE EXTERNAL DATA SOURCE (TRANSACT-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)。
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用数据库范围的凭据，其全局查询功能。 这在多个数据库分片是查询的能力。  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用数据库范围的凭据将扩展的事件文件写入到 Azure blob 存储。  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用数据库弹性池的范围的凭据。 有关详细信息，请参阅[克服使用弹性数据库爆炸性增长](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)  

- [大容量插入](../../t-sql/statements/bulk-insert-transact-sql.md)和[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)使用数据库范围的凭据来访问 Azure blob 存储中的数据。 有关详细信息，请参阅[示例的大容量访问 Azure Blob 存储中的数据](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。 
  
## <a name="permissions"></a>Permissions  
 需要**控件**对数据库拥有权限。  
  
## <a name="examples"></a>示例  
### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>A. 创建数据库范围的应用程序的凭据。
 下面的示例创建数据库范围的凭据调用`AppCred`。 数据库范围凭据包含 Windows 用户`Mary5`和密码。  
  
```tsql  
-- Create a db master key if one does not already exist, using your own password.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';  
  
-- Create a database scoped credential.  
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>B. 创建数据库范围的共享的访问签名的凭据。   
下面的示例创建数据库范围的凭据可以用于创建[外部数据源](../../t-sql/statements/create-external-data-source-transact-sql.md)，这可以执行大容量操作，如[大容量插入](../../t-sql/statements/bulk-insert-transact-sql.md)和[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).   
```tsql
CREATE DATABASE SCOPED CREDENTIAL MyCredentials  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```
  
### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. 创建数据库范围的 PolyBase 连接到 Azure 数据湖存储的凭据。  
下面的示例创建数据库范围的凭据可以用于创建[外部数据源](../../t-sql/statements/create-external-data-source-transact-sql.md)，可由 Azure SQL 数据仓库中的 PolyBase。

Azure 数据湖存储用于服务到服务身份验证使用 Azure Active Directory 应用程序。
请[创建 AAD 应用程序](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)和记录 client_id、 OAuth_2.0_Token_EndPoint 和密钥，再尝试创建数据库范围的凭据。

```tsql
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>'
    SECRET = '<key>'
;
```  
  
  
  
## <a name="more-information"></a>详细信息  
 [凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

