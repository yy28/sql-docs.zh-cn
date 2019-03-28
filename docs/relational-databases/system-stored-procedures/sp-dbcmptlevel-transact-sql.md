---
title: sp_dbcmptlevel (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96bd1aa87dba90963588db74935294c0dcdd8f0b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527420"
---
# <a name="spdbcmptlevel-transact-sql"></a>sp_dbcmptlevel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将某些数据库行为设置为与指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本兼容。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 使用[ALTER DATABASE 兼容级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>参数  
`[ @dbname = ] name` 是为其更改兼容级别的名称。 数据库名称必须符合标识符的规则。 *名称*是**sysname**，默认值为 NULL。  
  
`[ @new_cmptlevel = ] version` 是的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与数据库进行兼容。 *版本*是**tinyint**，默认值为 NULL。 该值必须为下列值之一：  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 如果未不指定任何参数，或如果*名称*未指定参数， **sp_dbcmptlevel**返回错误。  
  
 如果*名称*指定不带*版本*，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]返回一条消息，显示指定的数据库的当前兼容性级别。  
  
## <a name="remarks"></a>备注  
 有关兼容级别的说明，请参阅[ALTER DATABASE 兼容性级别&#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="permissions"></a>权限  
 数据库所有者、 的成员**sysadmin**固定服务器角色，并**db_owner**固定的数据库角色 （如果要更改当前数据库） 可以执行此过程。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [保留关键字 (Transact-SQL)](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
