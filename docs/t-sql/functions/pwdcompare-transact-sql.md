---
title: PWDCOMPARE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PWDCOMPARE
- PWDCOMPARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sa account
- passwords [SQL Server], blank
- PWDCOMPARE function [Transact-SQL]
ms.assetid: 5f84ff9e-c1ec-46aa-8501-50f854ebcc3a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 23b90a0d4a09fc2eb754dc5f298883ef4469ade5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="pwdcompare-transact-sql"></a>PWDCOMPARE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对密码执行哈希操作并将该哈希与现有密码的哈希进行比较。 PWDCOMPARE 可用于搜索空的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录密码或常见的弱密码。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
PWDCOMPARE ( 'clear_text_password'  
   , password_hash   
   [ , version ] )  
```  
  
## <a name="arguments"></a>参数  
 **'** *clear_text_password* **'**  
 未加密的密码。 clear_text_password 是 sysname (nvarchar(128))。  
  
 *password_hash*  
 密码的加密哈希。 password_hash 是 varbinary(128)。  
  
 *version*  
 已过时参数；如果 password_hash 表示来自早于 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]（已迁移到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本但从未转换为 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 系统）的登录名的值，则该参数可设置为 1。 version 是 int。  
  
> [!CAUTION]  
>  此参数用于向后兼容，但由于密码哈希 blob 现在包含自身的版本说明，因此忽略此参数。 [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
 如果 clear_text_password 的哈希与 password_hash 相匹配，则返回 1；反之，则返回 0。  
  
## <a name="remarks"></a>Remarks  
 PWDCOMPARE 函数不会威胁密码哈希的能力，因为可通过尝试使用作为第一个参数提供的密码登录，执行相同的测试。  
  
 PWDCOMPARE 不能与包含数据库用户的密码一起使用。 没有等效的包含数据库。  
  
## <a name="permissions"></a>权限  
 PWDENCRYPT 向用户开放使用。  
  
 检查 sys.sql_logins 的 password_hash 列要求 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-identifying-logins-that-have-no-passwords"></a>A. 标识没有密码的登录名  
 下面的示例标识没有密码的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('', password_hash) = 1 ;  
```  
  
### <a name="b-searching-for-common-passwords"></a>B. 搜索常见密码  
 为了搜索您要标识和更改的常见密码，请将密码指定为第一个参数。 例如，执行以下语句以便搜索指定为 `password` 的密码。  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('password', password_hash) = 1 ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [PWDENCRYPT (Transact-SQL)](../../t-sql/functions/pwdencrypt-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
