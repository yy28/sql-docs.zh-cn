---
title: sys.fn_translate_permissions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_translate_permissions
- sys.fn_translate_permissions_TSQL
- fn_translate_permissions
- fn_translate_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions bitmask [SQL Server]
- sys.fn_translate_permissions function
- fn_translate_permissions function
ms.assetid: ac97121f-2bd0-4f71-8e45-42c8584edbc5
author: rothja
ms.author: jroth
ms.openlocfilehash: c08fd2235750a8a7be99b5290813331141ddf0de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055371"
---
# <a name="sysfntranslatepermissions-transact-sql"></a>sys.fn_translate_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将 SQL 跟踪返回的权限位掩码翻译成权限名称表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>参数  
 *level*  
 应用该权限的安全对象的种类。 *级别*是**nvarchar(60)** 。  
  
 *perms*  
 权限列中返回的位掩码。 *perms*是**varbinary(16)** 。  
  
## <a name="returns"></a>返回  
 **table**  
  
## <a name="remarks"></a>备注  
 中返回的值**权限**的 SQL 跟踪列是由一个位掩码的整数表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于计算有效权限。 25 种安全对象中的每一种都有它自己的权限集，并且这些权限具有相应的数字值。 **sys.fn_translate_permissions**将此位掩码翻译成权限名称表。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="example"></a>示例  
 下面的查询使用`sys.fn_builtin_permissions`若要显示的权限，适用于的证书，然后使用`sys.fn_translate_permissions`来返回结果的权限位掩码。  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>请参阅  
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [sys.server_permissions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
