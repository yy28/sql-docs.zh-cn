---
title: sp_dropextendedproc (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3690d4c954ae3cde5159100280597af14a796d3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529759"
---
# <a name="spdropextendedproc-transact-sql"></a>sp_dropextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除扩展存储过程。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用 [CLR 集成](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>参数  
`[ @functname = ] 'procedure'` 是要删除的扩展存储过程的名称。 *过程*是**nvarchar(517)**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 执行**sp_dropextendedproc**删除中的用户定义的扩展存储的过程名称[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目录视图和移除的项从[sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md)目录视图。 仅在运行此存储的过程**主**数据库。  
  
**sp_dropextendedproc**不会删除系统扩展存储的过程。 相反，系统管理员应拒绝针对扩展存储过程的 EXECUTE 权限**公共**角色。  
  
 **sp_dropextendedproc**不能在事务内执行。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_dropextendedproc**。  
  
## <a name="examples"></a>示例  
 以下示例删除 `xp_hello` 扩展存储过程。  
  
> [!NOTE]  
>  该扩展存储过程必须已经存在，否则示例将返回错误消息。  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
