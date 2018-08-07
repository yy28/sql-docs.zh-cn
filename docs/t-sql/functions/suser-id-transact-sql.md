---
title: SUSER_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 572e9953ad74f4e2649d35d5b52a7eb8c26671dd
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452181"
---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  返回用户的登录标识号。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
> [!NOTE]  
>  从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，SUSER_ID 返回在 **sys.server_principals** 目录视图中作为 **principal_id** 列出的值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>参数  
 'login'  
 用户的登录名。 login 是 **nchar**。 如果 login 指定为 **char**，则 login 会隐式转换为 **nchar**。 login 可以是有权限连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或 Windows 用户或组。 如果未指定 login，则返回当前用户的登录标识号。 如果此参数包含词 NULL，将返回 NULL。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 SUSER_ID 仅为已经在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中显式提供的登录名返回标识号。 此 ID 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中用于跟踪所有权和权限。 此 ID 不等同于 SUSER_SID 返回的登录名的 SID。 如果 login 是 SQL Server 登录名，则 SID 映射到 GUID。 如果 login 是 Windows 登录名或 Windows 组，则 SID 映射到 Windows 安全标识符。  
  
 SUSER_SID 只返回在 syslogins 系统表中有条目的登录名的 SUID。  
  
 系统函数可以在选择列表、WHERE 子句和任何允许使用表达式的地方使用，并且后面必须始终跟随圆括号，即使未指定任何参数。  
  
## <a name="examples"></a>示例  
 下面的示例将返回 `sa` 登录名的登录标识号。  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID (Transact-SQL)](../../t-sql/functions/suser-sid-transact-sql.md)   
 [系统函数 (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
