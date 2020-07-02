---
title: sys. fn_translate_permissions （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: c3d7a464f3faba633dd09be12ef4c3d006ef19ef
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738589"
---
# <a name="sysfn_translate_permissions-transact-sql"></a>sys.fn_translate_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  将 SQL 跟踪返回的权限位掩码翻译成权限名称表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>自变量  
 *级别*  
 应用该权限的安全对象的种类。 *级别*为**nvarchar （60）**。  
  
 *perms*  
 权限列中返回的位掩码。 *perms*为**varbinary （16）**。  
  
## <a name="returns"></a>返回  
 **table**  
  
## <a name="remarks"></a>备注  
 SQL 跟踪的**权限**列中返回的值是用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来计算有效权限的位掩码的整数表示形式。 25 种安全对象中的每一种都有它自己的权限集，并且这些权限具有相应的数字值。 **sys. fn_translate_permissions**将此位掩码转换为权限名称表。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="example"></a>示例  
 下面的查询使用 `sys.fn_builtin_permissions` 来显示应用于证书的权限，然后使用 `sys.fn_translate_permissions` 返回权限位掩码的结果。  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>另请参阅  
 [权限 &#40;数据库引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys. server_permissions &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
