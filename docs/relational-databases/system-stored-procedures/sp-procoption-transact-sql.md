---
title: sp_procoption （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8ac7eae727206e0ad9b236229dbfca009529e3d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645832"
---
# <a name="sp_procoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  设置或清除自动执行的存储过程。 每次启动实例时，都将运行设置为自动执行的存储过程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>自变量  
`[ @ProcName = ] 'procedure'`要为其设置选项的过程的名称。 *过程*为**nvarchar （776）**，无默认值。  
  
`[ @OptionName = ] 'option'`要设置的选项的名称。 *选项*的唯一值为 "**启动**"。  
  
`[ @OptionValue = ] 'value'`指示是将选项设置为启用（**true**或**on**）还是禁用（**false**或**off**）。 *值*为**varchar （12）**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或错误号（失败）  
  
## <a name="remarks"></a>备注  
 启动过程必须在**master**数据库中，并且不能包含输入参数或输出参数。 所有数据库恢复后将开始执行存储过程，并在开始时记录“恢复已完成”消息。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例设置过程自动执行。  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'   
    , @OptionName = 'startup'   
    , @OptionValue = 'on';   
```  
  
 下面的示例阻止过程自动执行。  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'      
    , @OptionName = 'startup'
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>另请参阅  
 [执行存储过程](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
