---
title: sp_helpextendedproc (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43d9180ace10e61bbb9a9e65f48e718b8b426ea8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763875"
---
# <a name="sphelpextendedproc-transact-sql"></a>sp_helpextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告当前定义的扩展存储过程，以及该过程（函数）所属的动态链接库 (DLL) 的名称。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用 [CLR 集成](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@funcname =**] **'***过程*****  
 要报告其信息的扩展存储过程的名称。 *过程*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|扩展存储过程的名称。|  
|**dll**|**nvarchar(255)**|DLL 的名称。|  
  
## <a name="remarks"></a>备注  
 当*过程*指定，则**sp_helpextendedproc**上指定的报表扩展存储的过程。 如果未提供此参数， **sp_helpextendedproc**所属的返回所有扩展存储的过程名称和每个扩展存储的过程 DLL 名称。  
  
## <a name="permissions"></a>Permissions  
 若要执行的权限**sp_helpextendedproc**授予**公共**。  
  
## <a name="examples"></a>示例  
  
### <a name="a-reporting-help-on-all-extended-stored-procedures"></a>A. 报告所有扩展存储过程的帮助  
 以下示例将对所有扩展存储过程进行报告。  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc;  
GO  
```  
  
### <a name="b-reporting-help-on-a-single-extended-stored-procedure"></a>B. 报告单个扩展存储过程的帮助  
 以下示例报告`xp_cmdshell`扩展存储的过程。  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
