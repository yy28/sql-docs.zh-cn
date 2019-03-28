---
title: sp_delete_maintenance_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_maintenance_plan
- sp_delete_maintenance_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan
ms.assetid: 6f36b63f-3d18-4d42-9469-2febb6926530
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9952e41f51e20f2dffa037bc98b5007b111d32c9
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528269"
---
# <a name="spdeletemaintenanceplan-transact-sql"></a>sp_delete_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除指定的维护计划。  
  
> [!NOTE]  
>  数据库维护计划使用这些存储过程。 但此功能已由不使用此存储过程的维护计划取代。 可使用此过程对从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级的安装维护数据库维护计划。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_maintenance_plan [ @plan_id = ] 'plan_id'   
```  
  
## <a name="arguments"></a>参数  
`[ @plan_id = ] 'plan\_id'` 指定要删除的维护计划的 ID。 *plan_id*是**uniqueidentifier**，并且必须是有效的 id。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_delete_maintenance_plan**必须从运行**msdb**数据库。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_delete_maintenance_plan**。  
  
## <a name="examples"></a>示例  
 通过使用创建的维护计划中删除**sp_add_maintenance_plan**。  
  
```  
EXECUTE sp_delete_maintenance_plan 'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>请参阅  
 [维护计划](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [数据库维护计划存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
