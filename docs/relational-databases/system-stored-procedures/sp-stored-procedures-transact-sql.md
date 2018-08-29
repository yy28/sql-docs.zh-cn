---
title: sp_stored_procedures (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_stored_procedures_TSQL
- sp_stored_procedures
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stored_procedures
ms.assetid: fe52dd83-000a-4665-83fb-7a0024193dec
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 001a3476555b82c5262af4ff59cd70f5b88a0c5e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024663"
---
# <a name="spstoredprocedures-transact-sql"></a>sp_stored_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回当前环境中的存储过程列表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_stored_procedures [ [ @sp_name = ] 'name' ]   
    [ , [ @sp_owner = ] 'schema']   
    [ , [ @sp_qualifier = ] 'qualifier' ]  
    [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@sp_name =** ] **'***name***'**  
 用于返回目录信息的过程名。 *名称*是**nvarchar(390)**，默认值为 NULL。 支持通配符模式匹配。  
  
 [  **@sp_owner =** ] **'***架构*****  
 过程所属架构的名称。 *架构*是**nvarchar(384)**，默认值为 NULL。 支持通配符模式匹配。 如果*所有者*未指定，则遵循基础 dbms 的默认过程可见性规则将应用。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果当前架构包含具有指定名称的过程，则返回此过程。 如果指定了非限定存储过程，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]按以下顺序搜索此过程：  
  
-   当前数据库的 **sys** 架构。  
  
-   调用方的默认架构（在使用批或动态 SQL 执行时）；或者，如果非限定的过程名称出现在另一个过程定义的主体中，则接着搜索包含这一过程的架构。  
  
-   当前数据库中的 **dbo** 架构。  
  
 [  **@qualifier =** ] **'***限定符*****  
 过程限定符的名称。 *限定符*是**sysname**，默认值为 NULL。 多种 DBMS 产品支持窗体中的表的三部分命名方式 (*限定符 ***。*** 架构 ***。*** 名称*。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，*限定符*表示数据库名称。 在某些产品中，它表示表所在数据库环境的服务器名称。  
  
 [  **@fUsePattern =** ] **'***fUsePattern*****  
 确定是否将下划线 (_)、百分号 (%) 或 方括号 ([ ]) 解释为通配符。 *fUsePattern*是**位**，默认值为 1。  
  
 **0** = 启用模式匹配为关闭状态。  
  
 **1** = 启用模式匹配为打开状态。  
  
## <a name="return-code-values"></a>返回代码值  
 None  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|过程限定符名称。 该列可以为 NULL。|  
|**PROCEDURE_OWNER**|**sysname**|过程所有者名称。 该列始终返回值。|  
|**过程名称**|**nvarchar(134)**|过程名。 该列始终返回值。|  
|**NUM_INPUT_PARAMS**|**int**|保留供将来使用。|  
|**NUM_OUTPUT_PARAMS**|**int**|保留供将来使用。|  
|**NUM_RESULT_SETS**|**int**|保留供将来使用。|  
|**备注**|**varchar(254)**|对过程的说明。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不为此列返回值。|  
|**PROCEDURE_TYPE**|**smallint**|过程类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 始终返回 2.0。 此值可以为下列值之一：<br /><br /> 0 = SQL_PT_UNKNOWN<br /><br /> 1 = SQL_PT_PROCEDURE<br /><br /> 2 = SQL_PT_FUNCTION|  
  
## <a name="remarks"></a>Remarks  
 为了获得最大互操作性，网关客户端应只采用 SQL 标准模式匹配（百分号 (%) 和下划线 (_) 通配符）。  
  
 由于不就当前用户对特定存储过程执行访问的权限信息进行必要的检查，因此访问得不到保证。 请注意只使用三部分命名。 这表示在对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行时，只返回本地存储过程而不返回要求四部分命名的远程存储过程。 如果服务器特性 ACCESSIBLE_SPROC 为 Y 结果集中**sp_server_info**，仅可由当前用户执行的存储的过程返回。  
  
 **sp_stored_procedures**等效于**SQLProcedures** ODBC 中。 返回的结果按排序**PROCEDURE_QUALIFIER**， **PROCEDURE_OWNER**，并**PROCEDURE_NAME**。  
  
## <a name="permissions"></a>Permissions  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-all-stored-procedures-in-the-current-database"></a>A. 返回当前数据库中的所有存储过程  
 以下示例返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的所有存储过程。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_stored_procedures;  
```  
  
### <a name="b-returning-a-single-stored-procedure"></a>B. 返回单个存储过程  
 以下示例返回 `uspLogError` 存储过程的结果集。  
  
```  
USE AdventureWorks2012;  
GO  
sp_stored_procedures N'uspLogError', N'dbo', N'AdventureWorks2012', 1;  
```  
  
## <a name="see-also"></a>请参阅  
 [目录存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
