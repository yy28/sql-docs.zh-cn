---
title: xp_enumgroups （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 885e29f8abbeb185017bc2472566e41596a56900
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68116772"
---
# <a name="xp_enumgroups-transact-sql"></a>xp_enumgroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供 Microsoft Windows 本地组列表或在指定 Windows 域中定义的全局组列表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>参数  
 **"** *domain_name* **"**  
 要枚举其全局组列表的 Windows 域的名称。 *domain_name*的默认值为**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**组**|**sysname**|Windows 组的名称|  
|**条**|**sysname**|Windows 提供的 Windows 组的说明|  
  
## <a name="remarks"></a>备注  
 如果*domain_name*是运行实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的基于 Windows 的计算机的名称，或者未指定域名，则**xp_enumgroups**从运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的计算机枚举本地组。  
  
 **** 当的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例在 Windows 98 上运行时，不能使用 xp_enumgroups。  
  
## <a name="permissions"></a>权限  
 需要**master**数据库中**db_owner**固定数据库角色的成员身份或**sysadmin**固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例列出 `sales` 域中的组。  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的常规扩展存储过程](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
