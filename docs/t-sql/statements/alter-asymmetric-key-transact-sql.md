---
title: "更改非对称密钥 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ASYMMETRIC_KEY_TSQL
- ALTER ASYMMETRIC KEY
dev_langs: TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- passwords [SQL Server], asymmetric keys
- encryption [SQL Server], asymmetric keys
- DECRYPTION BY PASSWORD option
- ALTER ASYMMETRIC KEY statement
- asymmetric keys [SQL Server], modifying
ms.assetid: 958e95d6-fbe6-43e8-abbd-ccedbac2dbac
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13acb5d893188d08d8855d755c89cf9672eee066
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="alter-asymmetric-key-transact-sql"></a>ALTER ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  更改非对称密钥的属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ALTER ASYMMETRIC KEY Asym_Key_Name <alter_option>  
  
<alter_option> ::=  
      <password_change_option>   
    | REMOVE PRIVATE KEY   

<password_change_option> ::=  
    WITH PRIVATE KEY ( <password_option> [ , <password_option> ] )  

<password_option> ::=  
      ENCRYPTION BY PASSWORD = 'strongPassword'  
    | DECRYPTION BY PASSWORD = 'oldPassword'  
```  
  
## <a name="arguments"></a>参数  
 *Asym_Key_Name*  
 非对称密钥在数据库中所使用的名称。  
  
 REMOVE PRIVATE KEY   
 从非对称密钥中删除私钥，但不删除公钥。  
  
 WITH PRIVATE KEY  
 更改私钥的保护。  
  
 ENCRYPTION BY PASSWORD **=***stongPassword*  
 指定用于保护私钥的新密码。 *密码*必须符合 Windows 密码策略要求的计算机的运行的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果省略该选项，则使用数据库主密钥对私钥进行加密。  
  
 DECRYPTION BY PASSWORD **=***oldPassword*  
 指定当前用于保护私钥的旧密码。 如果私钥使用数据库主密钥进行加密，则不需要指定旧密码。  
  
## <a name="remarks"></a>注释  
 如果没有 ENCRYPTION BY PASSWORD 选项所需的数据库主密钥，并且未提供任何密码，则该操作将失败。 有关如何创建数据库主密钥的信息，请参阅[CREATE MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 您可以按下表所示，指定 PRIVATE KEY 选项，然后使用 ALTER ASYMMETRIC KEY 更改私钥的保护。  
  
|更改其保护|ENCRYPTION BY PASSWORD|DECRYPTION BY PASSWORD|  
|----------------------------|----------------------------|----------------------------|  
|旧密码到新密码|必需|必需|  
|密码到主密钥|省略|必需|  
|主密钥到密码|必需|省略|  
  
 必须首先打开数据库主密钥，然后才能使用它来保护私钥。 有关详细信息，请参阅[OPEN MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md).  
  
 若要更改的非对称密钥的所有权，使用[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 如果要删除私钥，则要求对非对称密钥具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-password-of-the-private-key"></a>A. 更改私钥的密码  
 以下示例更改用于保护非对称密钥 `PacificSales09` 的私钥的密码。 新密码为 `<enterStrongPasswordHere>`。  
  
```  
ALTER ASYMMETRIC KEY PacificSales09   
    WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<oldPassword>',  
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>');  
GO  
```  
  
### <a name="b-removing-the-private-key-from-an-asymmetric-key"></a>B. 从非对称密钥中删除私钥  
 以下示例从 `PacificSales19` 中删除私钥，只保留公钥。  
  
```  
ALTER ASYMMETRIC KEY PacificSales19 REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="c-removing-password-protection-from-a-private-key"></a>C. 从私钥中删除密码保护  
 以下示例从私钥中删除密码保护，然后使用数据库主密钥来保护该私钥。  
  
```  
OPEN MASTER KEY;  
ALTER ASYMMETRIC KEY PacificSales09 WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<enterStrongPasswordHere>' );  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [SQL Server 和数据库加密密钥（数据库引擎）](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [打开主密钥 &#40;Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [可扩展密钥管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
