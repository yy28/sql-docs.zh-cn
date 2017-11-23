---
title: "sp_add_maintenance_plan (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_maintenance_plan
- sp_add_maintenance_plan_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_maintenance_plan
ms.assetid: 01ab1834-6260-47cb-a1b7-20722217b062
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7868617e22111a843bbe3831adb014b3454f8760
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spaddmaintenanceplan-transact-sql"></a>sp_add_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加维护计划并返回计划 ID。  
  
> [!NOTE]  
>  数据库维护计划使用这些存储过程。 但此功能已由不使用此存储过程的维护计划取代。 可使用此过程对从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级的安装维护数据库维护计划。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_maintenance_plan [ @plan_name = ] 'plan_name' ,   
     @plan_id = 'plan_id' OUTPUT  
```  
  
## <a name="arguments"></a>参数  
 [  **@plan_name =**] *plan_name*  
 指定要添加的维护计划的名称。 *plan_name*是**varchar （128)**。  
  
 **@plan_id=** *plan_id*   
 指定维护计划的 ID。 *plan_id*是**uniqueidentifier**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 **sp_add_maintenance_plan**必须从运行**msdb**数据库并创建新的但为空，维护计划。 若要添加一个或多个数据库，并将其与作业或作业关联，执行**sp_add_maintenance_plan_db**和**sp_add_maintenance_plan_job**。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_add_maintenance_plan**。  
  
## <a name="examples"></a>示例  
 创建一个名为 Myplan 的维护计划。  
  
```  
DECLARE   @myplan_id UNIQUEIDENTIFIER;  
EXECUTE   sp_add_maintenance_plan N'Myplan',@plan_id=@myplan_id OUTPUT  
PRINT   'The id for the maintenance plan "Myplan" is:'+convert(varchar(256),@myplan_id);  
GO  
```  
  
 若成功创建了维护计划，则将返回计划 ID。  
  
```  
'The id for the maintenance plan "Myplan" is:' FAD6F2AB-3571-11D3-9D4A-00C04FB925FC  
```  
  
## <a name="see-also"></a>另请参阅  
 [维护计划](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [数据库维护计划存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
