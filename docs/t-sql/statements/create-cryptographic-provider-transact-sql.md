---
title: "创建加密提供程序 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_CRYPTOGRAPHIC_TSQL
- CRYPTOGRAPHIC PROVIDER
- PROVIDER_TSQL
- CREATE CRYPTOGRAPHIC
- CREATE CRYPTOGRAPHIC PROVIDER
- CRYPTOGRAPHIC_PROVIDER_TSQL
- CREATE_CRYPTOGRAPHIC_PROVIDER_TSQL
- PROVIDER
dev_langs:
- TSQL
helpviewer_keywords:
- 33085 (Database Engine error)
- CREATE CRYPTOGRAPHIC PROVIDER statement
- 33032 (Database Engine error)
ms.assetid: 059a39a6-9d32-4d3f-965b-0a1ce75229c7
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a7252786522ef4e0b4206db06d7dc8aa76cf308
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-cryptographic-provider-transact-sql"></a>CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  通过可扩展密钥管理 (EKM) 提供程序在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内创建加密提供程序。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE CRYPTOGRAPHIC PROVIDER provider_name   
    FROM FILE = path_of_DLL  
```  
  
## <a name="arguments"></a>参数  
 *provider_name*  
 可扩展密钥管理提供程序的名称。  
  
 *path_of_DLL*  
 实现 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可扩展的密钥管理接口的 .dll 文件的路径。 使用时**Microsoft Azure 密钥保管库的 SQL Server 连接器**默认位置是**适用于 Microsoft Azure 密钥 Vault\Microsoft.AzureKeyVaultService.EKM.dll C:\Program Files\Microsoft SQL Server 连接器'**.  
  
## <a name="remarks"></a>注释  
 提供程序创建的所有密钥都将按照提供程序的 GUID 引用提供程序。 在 DLL 的所有版本中都将保留此 GUID。  
  
 必须使用任何证书对实现 SQLEKM 接口的 DLL 进行数字签名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将验证此签名。 这包括其证书链，其必须具有安装在其根**受信任的根证书颁发机构**Windows 系统上的位置。 如果未正确验证签名，则 CREATE CRYPTOGRAPHIC PROVIDER 语句将失败。 有关证书和证书链的详细信息，请参阅[SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
 当 EKM 提供程序 DLL 未实现所有必需的方法时，CREATE CRYPTOGRAPHIC PROVIDER 可能返回错误 33085：  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 当用于创建 EKM 提供程序 DLL 的标头文件过期时，CREATE CRYPTOGRAPHIC PROVIDER 可能返回错误 33032：  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 权限或中的成员身份**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 下面的示例创建加密提供程序调用`SecurityProvider`中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从.dll 文件。 名为.dll 文件`c:\SecurityProvider\SecurityProvider_v1.dll`和服务器上安装。 必须首先在服务器上安装此提供程序的证书。  
  
```  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>另请参阅  
 [可扩展密钥管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER (Transact-SQL)](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [使用 Azure 密钥保管库的可扩展密钥管理 (SQL Server)](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  

