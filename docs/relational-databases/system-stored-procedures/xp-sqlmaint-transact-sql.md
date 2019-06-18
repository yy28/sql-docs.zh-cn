---
title: xp_sqlmaint (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2157462ca1f9509034f33208cce7aed2983ae4f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62644774"
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  调用**sqlmaint**实用程序使用一个字符串，包含**sqlmaint**开关。 **Sqlmaint**实用程序执行一系列一个或多个数据库上的维护操作。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>参数  
 **'** *switch_string* **'**  
 一个字符串，包含**sqlmaint**实用工具开关。 开关及其值之间必须以空格分隔。  
  
 **-？** 开关不能用于**xp_sqlmaint**。  
  
## <a name="return-code-values"></a>返回代码值  
 无。 如果返回错误**sqlmaint**实用程序将失败。  
  
## <a name="remarks"></a>备注  
 如果在使用 SQL Server 身份验证，登录用户调用此过程 **-U"***login_id***"** 并 **-P"***密码***"** 开关追加到前面*switch_string*之前执行。 如果使用 Windows 身份验证登录用户*switch_string*原样传递到**sqlmaint**。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 在以下示例中，`xp_sqlmaint` 调用 `sqlmaint` 执行完整性检查、创建报表文件并更新 `msdb.dbo.sysdbmaintplan_history`。  
  
```  
EXEC xp_sqlmaint '-D AdventureWorks2012 -PlanID 02A52657-D546-11D1-9D8A-00A0C9054212   
   -Rpt "C:\Program Files\Microsoft SQL Server\MSSQL\LOG\DBMaintPlan2.txt" -WriteHistory  -CkDB -CkAl';   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The command(s) executed successfully.  
```  
  
## <a name="see-also"></a>请参阅  
 [sqlmaint 实用工具](../../tools/sqlmaint-utility.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
