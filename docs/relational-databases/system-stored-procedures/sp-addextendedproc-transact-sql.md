---
title: sp_addextendedproc (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2083d370479fa19049a083ef401574f21740929c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spaddextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  注册新的名称扩展存储的过程以[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用 [CLR 集成](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>参数  
 [  **@functname =** ] *****过程*****  
 在动态链接库 (DLL) 内调用的函数名称。 *过程*是**nvarchar(517)**，无默认值。 *过程*选择可以在窗体中包含的所有者名称*owner.function*。  
  
 [  **@dllname =** ] *****dll*****  
 包含该函数的 DLL 名称。 *dll*是**varchar(255)**，无默认值。 建议指定 DLL 的完整路径。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 创建扩展存储的过程后，必须将它添加到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用**sp_addextendedproc**。 有关详细信息，请参阅[将扩展存储过程添加到 SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md)。  
  
 可以仅在运行此过程**master**数据库。 若要从数据库中而不执行扩展存储的过程**master**，限定的扩展存储过程名称**master**。  
  
 **sp_addextendedproc**将条目添加到[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目录视图中，注册新的名称扩展存储的过程替换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 它还添加了中的条目[sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md)目录视图。  
  
> [!IMPORTANT]  
>  升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后，未使用完整路径注册的现有 DLL 将无法工作。 若要解决此问题，请使用**sp_dropextendedproc**以注销该 DLL，然后重新注册其与**sp_addextendedproc**，指定的完整路径。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_addextendedproc**。  
  
## <a name="examples"></a>示例  
 下面的示例添加**xp_hello**扩展存储的过程。  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>另请参阅  
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT (Transact-SQL)](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
