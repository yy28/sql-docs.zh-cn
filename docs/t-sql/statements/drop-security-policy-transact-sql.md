---
title: "删除安全策略 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SECURITY_POLICY_TSQL
- DROP SECURITY POLICY
- DROP SECURITY
- DROP_SECURITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SECURITY POLICY statement
ms.assetid: 5bd3393d-2fa5-4db0-a69a-a1a72d638e9d
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 146d8d9341ae1d7c8cb63f4ebf186be95914a04f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-security-policy-transact-sql"></a>删除安全策略 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  删除安全策略。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP SECURITY POLICY [ IF EXISTS ] [schema_name. ] security_policy_name    
[;]  
```  
  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 仅当它已存在，则有条件地删除安全策略。  
  
 *schema_name*  
 是安全策略所属架构的名称。  
  
 *security_policy_name*  
 安全策略的名称。 安全策略名称必须符合有关标识符的规则，并且在数据库中以及对其架构来说必须是唯一的。  
  
## <a name="remarks"></a>注释  
  
## <a name="permissions"></a>Permissions  
 要求对架构具有 ALTER ANY SECURITY POLICY 权限和 ALTER 权限。  
  
## <a name="example"></a>示例  
  
```  
DROP SECURITY POLICY secPolicy;  
```  
  
## <a name="see-also"></a>另请参阅  
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [CREATE SECURITY POLICY (Transact-SQL)](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [ALTER SECURITY POLICY (Transact-SQL)](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [sys.security_policies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  

