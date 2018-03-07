---
title: "ALTER 凭据 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/19/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER CREDENTIAL
- ALTER_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], credentials
- credentials [SQL Server], ALTER CREDENTIAL statement
- modifying credentials
- authentication [SQL Server], credentials
- ALTER CREDENTIAL statement
ms.assetid: b08899a6-c09e-4af4-91aa-a978ada79264
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d01e5460b01790ba6b7ac59b25e7726399522165
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="alter-credential-transact-sql"></a>ALTER CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改凭据的属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>参数  
 *credential_name*  
 指定将要更改的凭据的名称。  
  
 标识**=***identity_name*  
 指定从服务器外部进行连接时要使用的帐户名称。  
  
 机密**=***机密*  
 指定发送身份验证所需的机密内容。 *机密*是可选的。  
  
## <a name="remarks"></a>注释  
 当更改凭据，这两者的值*identity_name*和*机密*将重置。 如果未指定可选参数 SECRET 的值，则存储的密码值将设置为 NULL。  
  
 使用服务主密钥对密码进行加密。 如果重新生成服务主密钥，则需要使用新服务主密钥对该密码重新加密。  
  
 有关凭据的信息会显示在**sys.credentials**目录视图。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY CREDENTIAL 权限。 如果该凭据是系统凭据，则要求具有 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-password-of-a-credential"></a>A. 更改凭据的密码  
 以下示例将更改存储在名为 `Saddles` 的凭据中的密码。 该凭据包含 Windows 登录名 `RettigB` 及其密码。 使用 SECRET 子句将新密码添加到凭据。  
  
```  
ALTER CREDENTIAL Saddles WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 删除凭据的密码  
 以下示例将删除名为 `Frames` 的凭据中的密码。 该凭据包含 Windows 登录名 `Aboulrus8` 和密码。 因为未指定 SECRET 选项，所以执行该语句后，凭据的密码为空。  
  
```  
ALTER CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
