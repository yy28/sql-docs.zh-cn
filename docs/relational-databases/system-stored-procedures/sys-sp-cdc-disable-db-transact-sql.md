---
title: sys.sp_cdc_disable_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_disable_db
- sys.sp_cdc_disable_db_TSQL
- sp_cdc_disable_db_TSQL
- sys.sp_cdc_disable_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_db
- sys.sp_cdc_disable_db
- change data capture [SQL Server], disabling databases
ms.assetid: 420fb99e-e60f-445b-b568-da96471f1e8f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0a3d2fb2eca31ed820665d89a68fdb814233a44c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672506"
---
# <a name="sysspcdcdisabledb-transact-sql"></a>sys.sp_cdc_disable_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对当前数据库禁用变更数据捕获。 并非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供变更数据捕获功能。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
sys.sp_cdc_disable_db  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sys.sp_cdc_disable_db**禁用变更数据捕获当前已启用的数据库中的所有表。 与变更数据捕获相关的所有系统对象（如更改表、作业、存储过程和函数）都将被删除。 **Is_cdc_enabled**列中的数据库条目[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图设置为 0。  
  
> [!NOTE]  
>  如果在禁用变更数据捕获时为数据库定义了很多捕获实例，则长时间运行事务可能导致 sys.sp_cdc_disable_db 的执行失败。 通过在运行 sys.sp_cdc_disable_db 之前使用 sys.sp_cdc_disable_table 禁用单个捕获实例，可以避免此问题。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下例对 `AdventureWorks2012` 数据库禁用变更数据捕获。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_db;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sys.sp_cdc_enable_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)   
 [sys.sp_cdc_disable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)  
  
  
