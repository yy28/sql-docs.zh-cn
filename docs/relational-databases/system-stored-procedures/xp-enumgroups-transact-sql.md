---
title: xp_enumgroups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 43366fd6463c885a41ad0304d45c2df1375015f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792045"
---
# <a name="xpenumgroups-transact-sql"></a>xp_enumgroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供 Microsoft Windows 本地组列表或在指定 Windows 域中定义的全局组列表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>参数  
 **'** *domain_name*   
 要枚举其全局组列表的 Windows 域的名称。 *domain_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**组**|**sysname**|Windows 组的名称|  
|**注释**|**sysname**|Windows 提供的 Windows 组的说明|  
  
## <a name="remarks"></a>备注  
 如果*domain_name*是基于 Windows 的计算机的名称的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是指定上，运行或没有域名，则**xp_enumgroups**枚举从计算机的本地组运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **xp_enumgroups**的实例时不能使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行于 Windows 98 上。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**db_owner**中的固定的数据库角色**主**数据库或中的成员身份**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例列出 `sales` 域中的组。  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [常规扩展存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
