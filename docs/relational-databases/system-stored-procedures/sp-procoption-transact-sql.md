---
title: sp_procoption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fcde4fd9439862dd88bdb1ff8c9eb40ff85ce0d4
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590421"
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
 [  **@ProcName =** ] **'**_过程_  
 是要为其设置选项的名称。 *过程*是**nvarchar(776)**，无默认值。  
  
 [  **@OptionName =** ] **'**_选项_  
 要设置的选项的名称。 唯一的值为*选项*是**启动**。  
  
 [  **@OptionValue =** ] **'**_值_  
 是否要选项设置为 on (**，则返回 true**或**上**) 或禁用 (**false**或者**关闭**)。 *值*是**varchar(12)**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或错误号（失败）  
  
## <a name="remarks"></a>备注  
 启动过程中必须是**主**数据库，并且不能包含输入或输出参数。 所有数据库恢复后将开始执行存储过程，并在开始时记录“恢复已完成”消息。  
  
## <a name="permissions"></a>权限  
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
  
## <a name="see-also"></a>请参阅  
 [执行存储过程](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
