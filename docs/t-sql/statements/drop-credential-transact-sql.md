---
title: "DROP CREDENTIAL (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/19/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP CREDENTIAL
- DROP_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing credentials
- DROP CREDENTIAL statement
- credentials [SQL Server], DROP CREDENTIAL statement
- authentication [SQL Server], credentials
- deleting credentials
- dropping credentials
ms.assetid: df22c826-317d-45a6-b078-186acb65f71e
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 99526bd72839ff483d39f0e78634ea27039388ae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-credential-transact-sql"></a>DROP CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从服务器中删除凭据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>参数  
 *credential_name*  
 要从服务器中删除的凭据的名称。  
  
## <a name="remarks"></a>注释  
 若要删除不删除凭据本身和凭据相关联的密钥，使用[ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md)。  
  
 有关凭据的信息会显示在**sys.credentials**目录视图。  
  
> [!WARNING]  
>  代理与凭据关联。 删除代理使用的凭据会让关联的代理处于不可用状态。 在删除代理使用的凭据时, 删除代理 (通过使用[sp_delete_proxy &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)并重新关联的代理创建使用[sp_add_proxy &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY CREDENTIAL 权限。 如果要删除系统凭据，则要求具有 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 以下示例删除名为 `Saddles` 的凭据。  
  
```  
DROP CREDENTIAL Saddles;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER 凭据 &#40;Transact SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

