---
title: sp_dropextendedproc （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ee41ad57e5c7e1e5bf13e7ad74b02d8fbecce6d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786925"
---
# <a name="sp_dropextendedproc-transact-sql"></a>sp_dropextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  删除扩展存储过程。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]请改用[CLR 集成](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>自变量  
`[ @functname = ] 'procedure'`要删除的扩展存储过程的名称。 *过程*为**nvarchar （517）**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 执行**sp_dropextendedproc**从[sys.databases](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目录视图中删除用户定义的扩展存储过程名称，并从[sys.databases. extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md)目录视图中删除该项。 此存储过程只能在**master**数据库中运行。  
  
**sp_dropextendedproc**不会删除系统扩展存储过程。 相反，系统管理员应对**公共**角色拒绝对扩展存储过程的 EXECUTE 权限。  
  
 无法在事务中执行**sp_dropextendedproc** 。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_dropextendedproc**执行。  
  
## <a name="examples"></a>示例  
 以下示例删除 `xp_hello` 扩展存储过程。  
  
> [!NOTE]  
>  该扩展存储过程必须已经存在，否则示例将返回错误消息。  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_addextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
