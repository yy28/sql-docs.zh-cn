---
title: sp_droptype （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droptype_TSQL
- sp_droptype
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droptype
ms.assetid: e78464ac-2370-4c4e-9cc0-06aebc07cec5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f6417edeacfd9462e5619e2844d4a162976d038b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783759"
---
# <a name="sp_droptype-transact-sql"></a>sp_droptype (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  从**systypes**中删除别名数据类型。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droptype [ @typename = ] 'type'  
```  
  
## <a name="arguments"></a>自变量  
`[ @typename = ] 'type'`您所拥有的别名数据类型的名称。 *类型*为**sysname**，无默认值。  
  
## <a name="return-code-type"></a>返回代码类型  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 如果表或其他数据库对象引用了**类型**别名数据类型，则不能将其删除。  
  
> [!NOTE]  
>  如果在表定义内使用某个别名数据类型，或者将某个规则或默认值绑定到这种数据类型，则不能删除它。  
  
## <a name="permissions"></a>权限  
 需要**db_owner**固定数据库角色的成员身份或**db_ddladmin**固定数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例删除别名数据类型 `birthday`。  
  
> [!NOTE]  
>  该别名数据类型必须已经存在，否则以下示例会返回错误消息。  
  
```  
USE master;  
GO  
EXEC sp_droptype 'birthday';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addtype &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md)   
 [sp_rename (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
