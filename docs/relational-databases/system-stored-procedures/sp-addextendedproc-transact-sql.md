---
title: sp_addextendedproc （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0bc8ea22699762927a026ae4cc811500c193555c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "68072756"
---
# <a name="sp_addextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将新扩展存储过程的名称注册到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]请改用[CLR 集成](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>参数  
`[ @functname = ] 'procedure'`在动态链接库（DLL）内调用的函数的名称。 *过程*为**nvarchar （517）**，无默认值。 *过程*可选择性地包含所有者名称形式的所有者名称 *。*  
  
`[ @dllname = ] 'dll'`包含该函数的 DLL 的名称。 *dll*的值为**varchar （255）**，无默认值。 建议指定 DLL 的完整路径。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 创建扩展存储过程后，必须使用**sp_addextendedproc**将其添加到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。 有关详细信息，请参阅[将扩展存储过程添加到 SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md)。  
  
 此过程只能在**master**数据库中运行。 若要从**master**之外的数据库中执行扩展存储过程，请使用**master**对扩展存储过程的名称进行限定。  
  
 **sp_addextendedproc**将条目添加到[sys.databases](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目录视图，并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]向注册新扩展存储过程的名称。 它还会在[sys. extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md)目录视图中添加一个条目。  
  
> [!IMPORTANT]  
>  升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后，未使用完整路径注册的现有 DLL 将无法工作。 若要更正此问题，请使用**sp_dropextendedproc**取消注册 DLL，然后使用**sp_addextendedproc**重新注册该 DLL，并指定完整路径。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_addextendedproc**执行。  
  
## <a name="examples"></a>示例  
 下面的示例将**xp_hello**扩展存储过程。  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>另请参阅  
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-sql&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-sql&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
