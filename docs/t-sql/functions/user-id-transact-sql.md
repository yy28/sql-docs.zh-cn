---
title: USER_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USER_ID
- USER_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- USER_ID function
- identification numbers [SQL Server]
- IDs [SQL Server], databases
- users [SQL Server], database ID numbers
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
ms.assetid: 67fd29bc-eda9-4d4d-b148-5d3659181a43
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1b8b1b0b5a9254382490272bd92405f52ed90a3d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67927609"
---
# <a name="user_id-transact-sql"></a>USER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回数据库用户的标识号。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用 [DATABASE_PRINCIPAL_ID](../../t-sql/functions/database-principal-id-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
USER_ID ( [ 'user' ] )  
```  
  
## <a name="arguments"></a>参数  
 user   
 要使用的用户名。 user 为 nchar   。 如果指定的是 char 类型的值，则将其隐式转换为 nchar   。 需要使用括号。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>备注  
 省略 user 时，则假定为当前用户  。 如果此参数包含词 NULL，将返回 NULL。当在 EXECUTE AS 之后调用 USER_ID 时，USER_ID 将返回模拟上下文的 ID。  
  
 当未映射到特定数据库用户的 Windows 主体使用组成员身份访问数据库时，USER_ID 将返回 0（public 的 ID）。 如果此类主体在不指定架构的情况下创建对象，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将创建映射到 Windows 主体的隐式用户和架构。 在这些情况下创建的用户不能用来连接到数据库。 映射到隐式用户的 Windows 主体调用 USER_ID 将返回该隐式用户的 ID。  
  
 USER_ID 可以在选择列表、WHERE 子句和任何允许使用表达式的地方使用。 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="examples"></a>示例  
 以下示例返回 `AdventureWorks2012` 用户 `Harold` 的标识号。  
  
```  
USE AdventureWorks2012;  
SELECT USER_ID('Harold');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [USER_NAME (Transact-SQL)](../../t-sql/functions/user-name-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [DATABASE_PRINCIPAL_ID (Transact-SQL)](../../t-sql/functions/database-principal-id-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
