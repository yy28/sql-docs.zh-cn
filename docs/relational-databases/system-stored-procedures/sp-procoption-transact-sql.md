---
title: "sp_procoption (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2906367b1f16c59ffbe4f4a98e25cf300302388
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spprocoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  设置或清除自动执行的存储过程。 设置为自动执行运行每次的实例的存储的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已启动。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>参数  
 [  **@ProcName =** ] *过程*  
 是为其设置选项的名称。 *过程*是**nvarchar(776)**，无默认值。  
  
 [  **@OptionName =** ] *选项*  
 要设置的选项的名称。 唯一值*选项*是**启动**。  
  
 [  **@OptionValue =** ] *值*  
 是，是否需要在设置选项 (**true**或**上**) 或禁用 (**false**或**关闭**)。 *值*是**varchar(12)**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或错误号（失败）  
  
## <a name="remarks"></a>注释  
 启动过程必须在**master**数据库中，并且不能包含输入或输出参数。 所有数据库恢复后将开始执行存储过程，并在开始时记录“恢复已完成”消息。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例设置过程自动执行。  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';   
```  
  
 下面的示例阻止过程自动执行。  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>另请参阅  
 [执行存储过程](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
