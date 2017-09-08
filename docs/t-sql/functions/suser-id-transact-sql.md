---
title: "SUSER_ID (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_ID_TSQL
- SUSER_ID
dev_langs:
- TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7e098c614f4e70cabf718ee4413920e61eb634c1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回用户的登录标识号。  
  
> [!NOTE]  
>  从开始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，SUSER_ID 返回的值作为列出**principal_id**中**sys.server_principals**目录视图。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>参数  
  *登录*   
 用户的登录名。 *登录名*是**nchar**。 如果*登录*指定为**char**，*登录*隐式转换为**nchar**。 *登录名*可以是任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或 Windows 用户或组有权连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*登录*是未指定，则返回当前用户的登录标识号。 如果此参数包含词 NULL，将返回 NULL。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 SUSER_ID 仅为已经在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中显式提供的登录名返回标识号。 此 ID 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中用于跟踪所有权和权限。 此 ID 不等同于 SUSER_SID 返回的登录名的 SID。 如果*登录*是 SQL Server 登录名，SID 映射到一个 GUID。 如果*登录*是 Windows 登录名或 Windows 组，该 SID 将映射到 Windows 安全标识符。  
  
 SUSER_SID 返回仅对有一个条目中的登录名 SUID **syslogins**系统表。  
  
 系统函数可以在选择列表、WHERE 子句和任何允许使用表达式的地方使用，并且后面必须始终跟随圆括号，即使未指定任何参数。  
  
## <a name="examples"></a>示例  
 下面的示例将返回 `sa` 登录名的登录标识号。  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40;Transact SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [系统函数 &#40;Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
